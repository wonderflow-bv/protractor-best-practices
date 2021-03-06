## Run and Debugging

### IDE Integration
**Problem**: The protractor tests are sanely difficult to debug

**Solution**: Having properly configured IDE with debug support (e.g. Intellij/Webstorm) can save many hours of pain. Just set a new run configuration according to the protractor's [manual](http://angular.github.io/protractor/#/debugging#setting-up-webstorm-for-debugging), and now you can debug your tests straight from IDE. The only small caveat: debugging doesn't work with enabled sharding capabilities.
![run-set](/images/run-set.png)
![run-debug](/images/run-debug.png)

### Element explorer & Elementor
**Problem**: Something weird is going on and something doesn't work.

**Solution**: Interactive debugging with [element explorer](http://angular.github.io/protractor/#/debugging#testing-out-protractor-interactively) where can type any protractor command. Launch the element explorer with the following code
```bash
webdriver-manager start
cd node_modules/protractor/bin
./elementexplorer.js
```

Additionally, you can use [elementor](https://github.com/andresdominguez/elementor) extension which works as a visualization tool (chrome extension) for element explorer.

### CI Integration
**Problem**: Run tests in CI

**Solution**: In case of CI, we can run our e2e tests on all major browsers and different OS's. For that purpose, we can use [Sauce Labs](https://saucelabs.com/) with credentials specified directly in protractor config file.
```js
export.config = {
	...
	sauceUser: process.env.SAUCE_USERNAME,
	sauceKey: process.env.SAUCE_ACCESS_KEY,
	capabilities['tunnel-identifier']: process.env.BUILD_NUMBER,
	...
}
```
If sauceKey and sauceUser are specified, seleniumServerJar will be ignored. The tests will run remotely via Sauce Labs.