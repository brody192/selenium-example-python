# This example is to be used with the [Browserless template](https://railway.app/template/browserless)

Create a reference variable on your Railway service that you deploy your app to -

```shell
BROWSER_WEBDRIVER_ENDPOINT=${{Browserless.BROWSER_WEBDRIVER_ENDPOINT}}
BROWSER_TOKEN=${{Browserless.BROWSER_TOKEN}}
```

</br>

Then use `os.environ['BROWSER_TOKEN']` and `os.environ['BROWSER_WEBDRIVER_ENDPOINT']` in code -

### Before

```python
chrome_options = webdriver.ChromeOptions()
# Set args similar to puppeteer's for best performance
chrome_options.add_argument("--window-size=1920,1080")
chrome_options.add_argument("--disable-background-timer-throttling")
chrome_options.add_argument("--disable-backgrounding-occluded-windows")
chrome_options.add_argument("--disable-breakpad")
chrome_options.add_argument("--disable-component-extensions-with-background-pages")
chrome_options.add_argument("--disable-dev-shm-usage")
chrome_options.add_argument("--disable-extensions")
chrome_options.add_argument("--disable-features=TranslateUI,BlinkGenPropertyTrees")
chrome_options.add_argument("--disable-ipc-flooding-protection")
chrome_options.add_argument("--disable-renderer-backgrounding")
chrome_options.add_argument("--enable-features=NetworkService,NetworkServiceInProcess")
chrome_options.add_argument("--force-color-profile=srgb")
chrome_options.add_argument("--hide-scrollbars")
chrome_options.add_argument("--metrics-recording-only")
chrome_options.add_argument("--mute-audio")
chrome_options.add_argument("--headless")
chrome_options.add_argument("--no-sandbox")

driver = webdriver.Chrome(
    options=chrome_options
)
```

### After

```python
chrome_options = webdriver.ChromeOptions()
chrome_options.set_capability('browserless:token', os.environ['BROWSER_TOKEN'])
# Set args similar to puppeteer's for best performance
chrome_options.add_argument("--window-size=1920,1080")
chrome_options.add_argument("--disable-background-timer-throttling")
chrome_options.add_argument("--disable-backgrounding-occluded-windows")
chrome_options.add_argument("--disable-breakpad")
chrome_options.add_argument("--disable-component-extensions-with-background-pages")
chrome_options.add_argument("--disable-dev-shm-usage")
chrome_options.add_argument("--disable-extensions")
chrome_options.add_argument("--disable-features=TranslateUI,BlinkGenPropertyTrees")
chrome_options.add_argument("--disable-ipc-flooding-protection")
chrome_options.add_argument("--disable-renderer-backgrounding")
chrome_options.add_argument("--enable-features=NetworkService,NetworkServiceInProcess")
chrome_options.add_argument("--force-color-profile=srgb")
chrome_options.add_argument("--hide-scrollbars")
chrome_options.add_argument("--metrics-recording-only")
chrome_options.add_argument("--mute-audio")
chrome_options.add_argument("--headless")
chrome_options.add_argument("--no-sandbox")

driver = webdriver.Remote(
    command_executor=os.environ['BROWSER_WEBDRIVER_ENDPOINT'],
    options=chrome_options
)
```

The rest of your code remains the same with no other changes required.