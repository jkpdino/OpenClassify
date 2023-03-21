# OpenClassify
Provides an interface to manually label data for AI/ML Training. Users can quickly and easily classify large datasets according to any number of categories using their command prompt.

## Features

- Load large datasets of text or images
- Create categories to group the data into
- Categorize data using keyboard shortcuts
- Save the categorized data as json

## Invocation

```
./classify data_set (-o output_file) (-f format) (-c config)
```

### Parameters

#### Data Set

Data set is a path of a folder containing data to be classified. Every file in the folder will be considered an item to be classified.

#### Output File

Output file is the location to save the JSON detailing the categories. If it is not provided, the system will prompt the user for an output file

#### Format

Data can be saved with groups as arrays containing the filenames of each file within it, known as Structure of Arrays, or as an object with filenames as keys, and the categories as values, known as Array of Structures.

These can be specified by using the `-f aos` or `-f soa` args to the script. If neither is specified, the program will prompt the user to specify one.

#### Config

The config file is the path of the file used to configure this classification. If no config is passed, then the program will allow the user to create one. The contents of the config file will be explained in the config section

## Interface

### Configuration Definition

If OpenClassify is started without a configuration file, it will prompt the user to create one. It will prompt the user for a list of schemes, terminated by entering an empty name. Then it will go through each scheme and ask for a list of categories. When it is done, classification will begin for each scheme.

### Classification

When classifying a file, it will be displayed at the top of the terminal, whether it is an image or text.

Underneath it are shortcuts which will classify it. These shortcuts look like this:

```
(1) Red
(2) Green
(3) Blue
```

When one of these keys is pressed, the next file will be loaded.

### Saving

After every file has been classified, OpenClassify will attempt to save the configuration file. If no filename is provided, it will prompt the user for one. If no format is provided, it will prompt the user for one.

If the file fails to save, OpenClassify will prompt the user for another file name.


## Config

The config file defines classification schemes, and the groups contained within them. The config file is a json file in this format:

```json
{
    "schemes": {
        "color": [ "Red", "Green", "Blue" ],
        "size": [ "Small", "Medium", "Large" ]
    }
}
```

## Output Data

Given the config file defined earlier, the output json might look like this:

### Array of Structures

```json
{
    "File1": {
        "color": "Red",
        "size": "Small",
    },
    "File2": {
        "color": "Green",
        "size": "Small",
    },
    "File3": {
        "color": "Blue",
        "size": "Medium",
    },
    "File4": {
        "color": "Red",
        "size": "Medium",
    },
    "File5": {
        "color": "Green",
        "size": "Large",
    },
    "File6": {
        "color": "Blue",
        "size": "Large",
    },
}
```



### Structure of Arrays

```json
{
    "size": {
        "Small": [
            "File1",
            "File2,"
        ],
        "Medium": [
            "File3",
            "File4",
        ],
        "Large": [
            "File5",
            "File6"
        ]
    },
    "color": {
        "Red": [
            "File1",
            "File4"
        ],
        "Green": [
            "File2",
            "File5",
        ],
        "Blue": [
            "File3",
            "File6"
        ]
    }
}
```