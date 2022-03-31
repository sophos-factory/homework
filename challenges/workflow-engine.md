# Workflow Engine

This assignment utilizes the Sophos Factory platform. You'll build one or more [step modules](https://docs.refactr.it/docs/reference/step-module-reference/) that execute a script in the language of your choice to solve the challenge.

The goal of this challenge is to implement a workflow engine that supports simple templating. Given the below JSON object, write two script modules:

1. A module that parses these instructions, and
2. A module that executes the workflow.

Create a [pipeline](https://docs.refactr.it/docs/building-pipelines/) that takes the below JSON as input, executes the instructions using your two modules above, and properly logs output to the run logs.

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

In addition to testing these scripts in Sophos Factory, add your code for the modules to the GitHub repository as described in the [Submission Instructions](../README.md#submission-instructions). If you have questions about how the code should work or multiple possible solutions, use your best judgement to choose a course of action. Document your decisions and justify them in your project README to help us understand your thought process.
