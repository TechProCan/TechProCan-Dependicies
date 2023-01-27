package Base;

import Utilities.ConfigReader;

import org.apache.commons.io.FileUtils;
import org.apache.logging.log4j.LogManager;
import org.apache.logging.log4j.Logger;
import org.openqa.selenium.*;
import org.openqa.selenium.interactions.Actions;
import org.openqa.selenium.support.ui.ExpectedCondition;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;
import org.testng.Assert;

import java.io.*;
import java.net.HttpURLConnection;
import java.net.URL;
import java.text.DateFormat;
import java.text.SimpleDateFormat;
import java.time.Duration;
import java.util.*;

import static Base.BaseTest.driver;
import static Base.BaseTest.getDriver;

import static org.testng.Assert.assertTrue;

public class BaseStepMethod {

    private static final Logger LOGGER = LogManager.getLogger(BaseStepMethod.class);
    private WebDriverWait wait;
    private String titleCSV;

    //Constructor
    public BaseStepMethod() {
        wait = new WebDriverWait(driver, Duration.ofSeconds(10));
    }

    protected String getCurrentURL() {
        return driver.getCurrentUrl();
    }

    protected void extractDataLayer() {
        Object x = ((JavascriptExecutor) driver).executeScript("return dataLayer");
    }

    protected WebElement waitVisibleByLocator(By locator) {
        WebElement element = null;

        try {
            element = wait.until(ExpectedConditions.visibilityOfElementLocated(locator));
        } catch (Exception e) {
            LOGGER.error("Web element is not visible!");
        }
        return element;
    }

    protected void AssertText(By locator, String text){
        Boolean element=null;
        try {
            element=wait.until(ExpectedConditions.textToBe(locator,text));
        }catch (Exception e){
            LOGGER.error("Text's value is not equals");
        }
    }
    protected void ContainsText(By locator,String text){
        Assert.assertTrue(getTextElement(locator).contains(text));
    }
    protected void AssertURL(String URL) {
        Boolean element = null;

        try {
            element = wait.until(ExpectedConditions.urlToBe(URL));
        } catch (Exception e) {
            // LOGGER.error("URL is not "+URL);
            //System.out.println(URL);
        }
    }
    protected void clickElement(By locator) {
        WebElement element = this.waitVisibleByLocator(locator);
        waitClickableByOfElement(element).click();
    }
    public static void waitForPageToLoad(Duration timeOutInSeconds) {
        ExpectedCondition<Boolean> expectation = new ExpectedCondition<Boolean>() {
            public Boolean apply(WebDriver driver) {
                return ((JavascriptExecutor) driver).executeScript("return document.readyState").equals("complete");
            }
        };
        try {
            System.out.println("Waiting for page to load...");
            WebDriverWait wait = new WebDriverWait(driver, timeOutInSeconds);
            wait.until(expectation);
        } catch (Throwable error) {
            LOGGER.error("Timeout waiting for Page Load Request to complete after " + timeOutInSeconds + " seconds");

        }
    }

    protected List<WebElement> waitAllVisibleByLocator(By locator) {
        List<WebElement> element = null;

        try {
            element = driver.findElements(locator);
        } catch (Exception e) {
            LOGGER.error("Web element is not visible!");
        }
        return element;
    }

    protected WebElement waitClickableByOfElement(WebElement webElement) {
        WebElement element = null;

        try {
            element = wait.until(ExpectedConditions.elementToBeClickable(webElement));
        } catch (Exception e) {
            LOGGER.error("Web element is not clickable!");
        }
        return element;
    }
    public static void waitFor(int sec) {
        try {
            Thread.sleep(sec * 1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    protected void hoverElement(By locator, int second) {
        Actions action = new Actions(driver);
        action.moveToElement(driver.findElement(locator)).pause(Duration.ofSeconds(second)).perform();

    }
    protected void selectElementVisibleText(By locator, String text) {
        Select select=new Select(driver.findElement(locator));
        select.selectByVisibleText(text);
    }
    protected void selectElementByIndex(By locator, int index) {
        Select select=new Select(driver.findElement(locator));
        select.selectByIndex(index);
    }

    protected WebElement waitPresenceOfElementByLocator(By locator) {
        WebElement element = null;

        try {
            element = wait.until(ExpectedConditions.presenceOfElementLocated(locator));
        } catch (Exception e) {
            LOGGER.error("Web element not found in document!");
        }
        return element;
    }

    protected void checkStatusNetwork() throws IOException {
        LOGGER.info("User connecting to the Http Network status of the page.");


        HttpURLConnection cn = (HttpURLConnection) new URL(driver.getCurrentUrl()).openConnection();

        cn.setRequestMethod("HEAD");
        cn.connect();
        Integer c = cn.getResponseCode();

        LOGGER.info(driver.getCurrentUrl() + " Http status code: " + c);


        Assert.assertFalse(c.toString().startsWith("4") || c.toString().startsWith("5"), c + "Invalid Link " + driver.getCurrentUrl());
        cn.disconnect();
    }

    protected void imgCheckStatusNetwork(String imgURL) throws IOException {
        LOGGER.info("Kullanıcı sayfanın img'in Network status'üne bağlanıyor.");

        try {
            HttpURLConnection cn = (HttpURLConnection) new URL(driver.getCurrentUrl())
                    .openConnection();

            cn.setRequestMethod("HEAD");
            cn.connect();
            Integer c = cn.getResponseCode();
            LOGGER.info(imgURL + " Http status code: " + c);


            Assert.assertFalse(c.toString().startsWith("4") || c.toString().startsWith("5"), c + "Broken pic " + imgURL);
            cn.disconnect();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    protected void checkStatusNetworkNotAssertion() throws IOException {
        LOGGER.info("Kullanıcı sayfanın Http Network status'üne bağlanıyor.");


        HttpURLConnection cn = (HttpURLConnection) new URL(driver.getCurrentUrl())
                .openConnection();

        cn.setRequestMethod("HEAD");
        cn.connect();
        Integer c = cn.getResponseCode();

        LOGGER.info(driver.getCurrentUrl() + " Http status code: " + c);


        cn.disconnect();

    }

    protected String getTextElement(By locator) {
        return waitPresenceOfElementByLocator(locator).getText();
    }

    protected WebElement setTextElement(By locator, String text) {
        WebElement element = waitPresenceOfElementByLocator(locator);
        element.clear();
        element.sendKeys(text);

        return element;
    }

    protected boolean isDisplayElement(By locator) {
        WebElement element = waitPresenceOfElementByLocator(locator);
        return element.isDisplayed();
    }

    protected boolean isEnableElement(By locator) {
        WebElement element = waitPresenceOfElementByLocator(locator);
        return element.isEnabled();
    }

    protected String getAttributeElement(By locator, String attribute) {
        WebElement element = this.waitVisibleByLocator(locator);
        return element.getAttribute(attribute);
    }

    protected void imgCheckStatusNetworkHttp(String imgURL) throws IOException {
        LOGGER.info("Kullanıcı sayfanın img'in Network status'üne bağlanıyor.");

        HttpURLConnection cn = (HttpURLConnection) new URL(imgURL).openConnection();
        cn.setRequestMethod("HEAD");
        cn.connect();
        Integer c = cn.getResponseCode();
        LOGGER.info(driver.getCurrentUrl() + " Http status code: " + c);

        Assert.assertFalse(c.toString().startsWith("4") || c.toString().startsWith("5"), c + "Invalid Link " + driver.getCurrentUrl());


    }

    protected void assertContains(Object actual, Object... expected) {
        assertTrue(Arrays.asList(expected).contains(actual), "text did not match");
    }

    protected void resultTakeScreenShot(String scenarioName) {
        takeScreenShot(scenarioName, false);
    }

    protected void errorMessage(String scenarioName, String message) {
        takeScreenShot(scenarioName, true);
        Assert.fail(message);
    }

    protected String dateTime() {
        DateFormat dateFormat = new SimpleDateFormat("dd MMMMM yyyy");
        Date date = new Date();
        String currentDate = dateFormat.format(date);
        return currentDate;

    }



    protected String getTabTitle() {
        return driver.getTitle();
    }

    // ========= JS METHODS =========== //

    // CLICK WITH JS
    protected void clickWithJS(WebElement element) {
        ((JavascriptExecutor) driver).executeScript("arguments[0].scrollIntoView(true);", element);
        ((JavascriptExecutor) driver).executeScript("arguments[0].click();", element);
    }

    // SCROLL TO ELEMENT WITH JS
    protected void scrollToElement(WebElement element) {
        ((JavascriptExecutor) driver).executeScript("arguments[0].scrollIntoView(true);", element);
    }

    // SET ATTRIBUTE WITH JS
    protected void setAttribute(WebElement element, String attributeName, String attributeValue) {
        ((JavascriptExecutor) driver).executeScript("arguments[0].setAttribute(arguments[1], arguments[2]);", element, attributeName, attributeValue);
    }


    // ===========  JS COMMAND EXECUTE  =========== //

    // EXECUTES THE GIVEN JAVASCRIPT command on given web element
    protected void executeJScommand(WebElement element, String command) {
        JavascriptExecutor jse = (JavascriptExecutor) driver;
        jse.executeScript(command, element);
    }

    protected void executeJScommand(String command) {
        JavascriptExecutor jse = (JavascriptExecutor) driver;
        jse.executeScript(command);
    }


    protected void cleanByJs(WebElement element) {
        JavascriptExecutor jse = (JavascriptExecutor) driver;
        jse.executeScript("arguments[0].value = '';", element);
    }

    protected void switchToWindow() {
        ArrayList<String> tabs2 = new ArrayList<String>(driver.getWindowHandles());
        driver.switchTo().window(tabs2.get(1));
    }

    protected String takeScreenShot(String methodName, boolean isFail) {

        try {
            String fail = isFail ? "FailTest" : "TestResult";
            SimpleDateFormat formatterDate = new SimpleDateFormat("yyyy-MM-dd_HH-mm");
            String time = formatterDate.format(new Date());

            String screenshotLoc = System.getProperty("user.dir") + File.separator + "ScreenshotFile" + File.separator + fail +
                    File.separator + time + "_" + methodName.replaceAll(" ", "") + ".png";

            File srcFiler = ((TakesScreenshot) getDriver()).getScreenshotAs(OutputType.FILE);

            FileUtils.copyFile(srcFiler, new File(screenshotLoc));
            return screenshotLoc;
        } catch (IOException e) {
            LOGGER.error("Error occurred in screenshot file operations!", e);

            Assert.fail(e.getMessage());

            return null;
        }
    }

}
