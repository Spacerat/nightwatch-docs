### Writing Tests

Using the preferred CSS selector model to locate elements on a page, Nightwatch makes it very easy to write automated End-to-End tests.

Create a separate folder for tests in your project, e.g.: `tests`. Each file inside it will be loaded as a test by the Nightwatch test runner. A basic test will look like this:

<div class="sample-test">
<pre data-language="javascript"><code class="language-javascript">
module.exports = {
  'Demo test Google' : function (browser) {
    browser
      .url('http://www.google.com')
      .waitForElementVisible('body', 1000)
      .setValue('input[type=text]', 'nightwatch')
      .waitForElementVisible('button[name=btnG]', 1000)
      .click('button[name=btnG]')
      .pause(1000)
      .assert.containsText('#main', 'Night Watch')
      .end();
  }
};</code></pre>
</div>
<br>
<p class="alert alert-warning">
Remember **always** to call the `.end()` method when you want to close your test, in order for the Selenium session to be properly closed.
</p>

A test can have multiple steps, if needed:

<div class="sample-test">
<pre data-language="javascript"><code class="language-javascript">
module.exports = {
  'step one' : function (browser) {
    browser
      .url('http://www.google.com')
      .waitForElementVisible('body', 1000)
      .setValue('input[type=text]', 'nightwatch')
      .waitForElementVisible('button[name=btnG]', 1000)
  },

  'step two' : function (browser) {
    browser
      .click('button[name=btnG]')
      .pause(1000)
      .assert.containsText('#main', 'Night Watch')
      .end();
  }
};</code></pre></div>

Tests can also be written in this format:

<div class="sample-test">
<pre data-language="javascript"><code class="language-javascript">
this.demoTestGoogle = function (browser) {
  browser
    .url('http://www.google.com')
    .waitForElementVisible('body', 1000)
    .setValue('input[type=text]', 'nightwatch')
    .waitForElementVisible('button[name=btnG]', 1000)
    .click('button[name=btnG]')
    .pause(1000)
    .assert.containsText('#main', 'The Night Watch')
    .end();
};</code></pre>
</div>

Note that the order of execution of these steps is not guarenteed, since an object's key ordering in Javascript is implementation dependant. In V8, steps with names that can be parsed as numbers will be run before any others. 
