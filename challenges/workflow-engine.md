# Workflow Engine

**Allotted Time:** 1 hour

The goal of this challenge is to implement a workflow engine that supports simple templating. Given the below JSON object, write a program that executes the workflow.

```json
{
  "tasks": [{
    "id": "one",
    "type": "print",
    "needs": [],
    "props": {
      "message": "Hello!"
    }
  },{
    "id": "two",
    "type": "subtract",
    "needs": ["three"],
    "props": {
      "num1": 21,
      "num2": "{{ tasks.three.result }}"
    }
  },{
    "id": "three",
    "type": "add",
    "needs": ["one"],
    "props": {
      "num1": 3,
      "num2": 6
    }
  }]
}
```

`id` is a unique identifier for each task.

`type` defines the action performed by the task.

`needs` specifies task dependencies. The task should not execute until all other tasks with `id` fields in the `needs` array have finished executing.

`props` are task type-specific input properties.

The `{{ }}` value on line 15 is an expression. Your engine should detect these props and evaluate the expression. Tasks that have already executed should contain an additional `result` field. `add` and `sub` type tasks should place their addition/subtraction result in this field.
