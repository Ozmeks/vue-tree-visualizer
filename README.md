# Vue.js Tree Visualizer

This project is a Vue.js application that allows users to visualize and edit a hierarchical structure from a JSON file. Each object in the JSON file has an `id` and a `parent_id`, representing the hierarchical relationship between the nodes.

## Features

- Load a hierarchical structure from a JSON file
- Visualize the structure as a tree
- Add new nodes to the tree
- Delete nodes from the tree

## Project setup
```
npm install
```

### Running the Project
```
npm run serve
```

### Example JSON File
Save the following content as example.json and use it to test the application:

```
[
    {"id": "root1"},
    {"id": "child1", "parent_id": "root1"},
    {"id": "child2", "parent_id": "root1"}
]
```
