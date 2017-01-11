# istanbul-reporter-shield-badge

Generates a shields.io url representing the coverage of your tests suit.
Also generates the markdown equivalent code.

## Install

> npm install --save-dev istanbul-reporter-shield-badge


## Usage

Register the report using the istanbul Report factory:

```javascript
var shieldBadgeReporter = require('istanbul-reporter-shield-badge');
var istanbul = require('istanbul');
istanbul.Report.register(shieldBadgeReporter);
```

Create a report after istanbul has collected coverage information:

```javascript
var report = require('istanbul').Report.create('shield-badge');
```

Add to your karma config file:

```javascript
config.set({
    reporters: ['coverage'],
    coverageReporter: {
      dir: './coverage',
      reporters: [
        { type: 'lcov', subdir: '.' },
        { type: 'text-summary' },
        { type: function() {
          var shieldBadgeReporter = require('istanbul-reporter-shield-badge')
          var istanbul = require('istanbul')
          istanbul.Report.register(shieldBadgeReporter)
          return 'shield-badge'
        }(), subdir: '.' }
      ]
    }
  })
```

### Config options
|name        |default                  |description                                                                                                               |
|------------|-------------------------|--------------------------------------------------------------------------------------------------------------------------|
|file        |coverage.shield.badge.md |the file where the url of the badge will be generated                                                                                                                          |
|subject     |coverage                 |the text that will appear on the left of the shield badge                                                                                                                          |
|range       |[50, 80]                 |must be a JavaScript Array representing medium and high levels of coverage                                                |
|coverageType|lines                    |must be one of: statements, lines, branches, functions; will be used to display the coverage percentage of the chosen type|

#### Karma Configuration File Example

```javascript
config.set({
    reporters: ['coverage'],
    coverageReporter: {
      dir: './coverage',
      reporters: [
        { type: 'lcov', subdir: '.' },
        { type: 'text-summary' },
        { type: function() {
                  var shieldBadgeReporter = require('istanbul-reporter-shield-badge')
                  var istanbul = require('istanbul')
                  istanbul.Report.register(shieldBadgeReporter)
                  return 'shield-badge'
                }(),
          subdir: '.',
          coverageType: 'statements',
          range: [50, 75],
          subject: 'Code Coverage'
        }
      ]
    }
  })
```

The example above will generate the following shields.io badge for a coverage percentage of 77.91% at the statements level: 
[![coverage](https://img.shields.io/badge/Code Coverage-77.91%25-yellow.svg)](https://img.shields.io/badge/Code Coverage-77.91%25-yellow.svg)

## LICENSE

MIT License

Copyright (c) 2017 

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
