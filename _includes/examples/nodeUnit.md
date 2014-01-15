{% highlight sh linenos %}
var webdriverjs = require('webdriverjs'),
    assert      = require('assert');
 
module.exports = {
 
    setUp: function (callback) {
        client = webdriverjs.remote({ desiredCapabilities: {browserName: 'phantomjs'} });
        client.init();
 
        callback();
    },
    test1: function (test) {
        client
            .url('https://github.com/')
            .getElementSize('.header-logo-wordmark', function(err, result) {
                test.ok(err === null, 'getElementSize() should cause no error');
                test.ok(result.height === 32, 'logo height should be 32px');
                test.ok(result.width  === 89, 'logo width should be 89px');
            })
            .getTitle(function(err, title) {
                test.ok(err === null, 'getTitle() should cause no error');
                test.ok(title === 'GitHub · Build software better, together.', 'title should be "GitHub · Build software better, together."');
            })
            .getElementCssProperty('css selector','a[href="/plans"]', 'color', function(err, result){
                test.ok(err === null, 'getElementCssProperty() should cause no error');
                test.ok(result === 'rgba(65,131,196,1)', 'color is "' + result + '" but should be "rgba(65,131,196,1)"');
            });
 
        test.done();
    },
    tearDown: function (callback) {
        // clean up
        client.end(callback);
    }
};
{% endhighlight %}
<footer>webdriverjs.with.nodeunit.js <a href="https://gist.github.com/christian-bromann/6416889" target="_blank">Open Gist</a></footer>