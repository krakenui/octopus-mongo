# octopus-mongo


[![NPM version][npm-image]][npm-url] [![npm download][download-image]][download-url]

[npm-image]: http://img.shields.io/npm/v/octopus-mongo.svg?style=flat-square
[npm-url]: http://npmjs.org/package/octopus-mongo
[download-image]: https://img.shields.io/npm/dm/octopus-mongo.svg?style=flat-square
[download-url]: https://npmjs.org/package/octopus-mongo

## Install

[![octopus-mongo](https://nodei.co/npm/octopus-mongo.png)](https://npmjs.org/package/octopus-mongo)

```
npm install --save octopus-mongo
```


## Features

```
- Define interface wrap for entity
- Define common dbcontext
- Define db connect hub
- Define base repository with repository pattern
```

## Install

- Before install require packages:

```
npm install mongoose@^5.9.3
```

- Install octopus-mongo

```
npm install octopus-mongo
```

## How it work

#### MongoDB context

- using:

```
import { connectMongoDb } from "octopus-mongo";

await connectMongoDb();
```

- output: `MongoDB connected...`

#### Repository pattern

- Define model schema:

```
import { Schema } from "mongoose";

const CategorySchema: Schema = new Schema({
  categoryId: {
    type: String,
    required: true,
  },
  parentId: {
    type: String,
  },
  name: {
    type: String,
    required: true,
  },
  context: {
    type: String,
    required: true,
  },
  active: {
    type: Boolean,
  },
  createdBy: {
    type: String,
  },
  updatedBy: {
    type: String,
  },
  createdTime: {
    type: Date,
  },
  updatedTime: {
    type: Date,
  },
});
```

- Define model instance:

```
const Category = model("categories", CategorySchema);
```

- Define entity interface:

```
import { IDocument } from "octopus-mongo";

interface ICategory extends IDocument<string> {
  categoryId: string;
  parentId: string;
  name: string;
  context: string;
  active: boolean;
  createdBy: string;
  updatedBy: string;
  createdTime: Date;
  updatedTime: Date;
}
```

- Declare repository into service to query:

```
import { Repository } from "octopus-mongo";

_categoryRepository = Repository<string, ICategory>(Category);

const allCategories = _categoryRepository.find({});
```
