# Folder and subfolder structure

Your project folder containing raw data will be structured in a hierarchical way following BIDS standards:
```
project/
└── subject/
    └── session/
        └── datatype
            └── run/
                ├── some_raw_data_file
                ├── some_preprocessed_data_file
                └── notes
```

Here is an example:
```
my_project/
└── subject/
    └── session/
        └── run/
            ├── some_raw_data_file
            ├── some_preprocessed_data_file
            └── notes
```
Folders will be named in lowercase, with words separated by underscores (`_`).
