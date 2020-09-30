# WorkflowDir file layout

In order to use WorkflowDir effectively, it is useful to understand
the conventional wfd file layout.

We will create a sample workspace to examine the layout.

## Creating a workflowdir workspace

```sh
$ wfd init
```

## Examine layout

```sh
$ find .
$ tree
.
├── dead
├── run.sh
├── todo
└── workflowdir.toml

2 directories, 2 files
```

- `workflowdir.toml` is the configuration of the workspace. It directs the command to be run, as well as where to look for work.
- `run.sh` is a "Hello, World!" example that's dropped in place. Feel free to remove it if you know what you want to do.
- `todo` is where all of the unfinished work lives.
- `dead` is to hold any files from `todo` that couldn't be processed correctly. To retry things in `dead`, just run `wfd retry` from the project root.
