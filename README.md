# mock-hubot-robot
Provides a mock robot context used to provide testing support for Hubot script development

### Install

```
npm install mock-hubot-robot
```

### Features
Currently only supports testing regex triggers

### Use

Assuming a file in a test folder off the root of your hubot source
Using Mocha and Chai

`some-test-file-name.js`
```js
require('coffee-script')
require('coffee-script/register')
var robotCtx = require('../')(),
    testscript = require('./testscript.coffee'),
    expect = require('chai').expect

describe('Testing that my robot hears correctly',function() {
  before(function(done) {
    //This is what binds the robot context into your script.
    testscript(robotCtx)
    done()
  })
  
  it('hears phrase "who\'s here"',function(done) {
    //Execute your phrase against all of the robot.hear bindings your script has made
    robotCtx.ExecHear("who's here?",function(matched) {
      expect(matched).to.be.true
      done()
    })
  })
})
```

`testscript.coffee`
```coffee
module.exports = (robot) ->
  robot.hear /who's here/, (res) ->
    console.log("called")
```

Output
```
  Testing that my robot hears correctly
    ✓ hears phrase "who's here"


  1 passing (11ms)

```