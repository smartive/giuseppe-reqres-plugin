# giuseppe request response plugin

This is a plugin for [giuseppe](http://giuseppe.smartive.ch) which adds a `@Req` and a `@Res` parameter definition.
Those definitions do inject the corresponding express object. `@Req` does inject the express request and `@Res` the
express response object. So you have full control over what you do in your routes.

Note that the `@Res` parameter has the `canHandleResponse` flag set to `true`. Which means you need to actually
handle the response in the route. Giuseppe won't run the result of your method through the return type handler.

##### A bunch of badges

[![Build Status](https://travis-ci.org/smartive/giuseppe-reqres-plugin.svg)](https://travis-ci.org/smartive/giuseppe-reqres-plugin)
[![npm](https://img.shields.io/npm/v/giuseppe-reqres-plugin.svg?maxAge=3600)](https://www.npmjs.com/package/giuseppe-reqres-plugin)
[![Coverage status](https://img.shields.io/coveralls/smartive/giuseppe-reqres-plugin.svg?maxAge=3600)](https://coveralls.io/github/smartive/giuseppe-reqres-plugin)

## Installation

To install this package, simply run

[![NPM](https://nodei.co/npm/giuseppe-reqres-plugin.png?downloads=true&stars=true)](https://nodei.co/npm/giuseppe-reqres-plugin/)

## How to use

This is an example for a request injection:
```typescript
import { Giuseppe, Controller, Get } from 'giuseppe';
import { GiuseppeReqResPlugin, Req } from 'giuseppe-reqres-plugin';
import { Request } from 'express';

@Controller()
class Ctrl{
    @Get()
    public func(@Req() request: Request): string {
        return request.get('Accept-Language'); // just return the string value of the header Accept-Language
    }
}

const app = new Giuseppe();
app.registerPlugin(new GiuseppeReqResPlugin());
app.start();
```

This is an example for a response injection:
```typescript
import { Giuseppe, Controller, Get } from 'giuseppe';
import { GiuseppeReqResPlugin, Res } from 'giuseppe-reqres-plugin';
import { Response } from 'express';

@Controller()
class Ctrl{
    @Get()
    public func(@Res() response: Response): void {
        request
            .send('Foobar')
            .status('404')
            .end();
    }
}

const app = new Giuseppe();
app.registerPlugin(new GiuseppeReqResPlugin());
app.start();
```

## Changelog

The changelog is based on [keep a changelog](http://keepachangelog.com) and is located here:

[Changelog](CHANGELOG.md)

## Licence

This software is licenced under the [MIT](LICENSE) licence.
