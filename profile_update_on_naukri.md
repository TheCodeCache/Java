# Profile Update Activity on https://naukri.com   

```java
package com.naukri.profile_update;

import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;
import java.util.HashMap;
import java.util.Map;
import java.util.Properties;

import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.edge.EdgeDriver;


/**
 * For better productivity
 * 
 * this code uploads a pdf file, a resume basically, to naukri.com
 * 
 * TODO - To make it resilient from failure, also in case of failure, it must
 * send a response w/o fail
 * 
 * @author TheCodeCache - Manoranjan
 */
public class Resume {

	private static String username = null;
	private static String password = null;
	private static WebDriver driver = null;

	private static boolean enable = false;

	private static Map<String, String> hardcodedURLs = new HashMap<>();

	static {
		System.out.println("Resume class Loading");
	}

	static {
		System.setProperty("webdriver.edge.driver", "D:\\workspace\\drivers\\msedgedriver.exe");
//		EdgeOptions options = new EdgeOptions();
//		options.addArguments("headless");
		if (enable)
			driver = new EdgeDriver();
	}

	static {
		hardcodedURLs.put("login", "https://www.naukri.com/nlogin/login");
		hardcodedURLs.put("profile", "https://www.naukri.com/mnjuser/profile?id=&altresid");
		hardcodedURLs.put("logout", "https://www.naukri.com/nlogin/logout");
	}

	static {
		try (InputStream input = new FileInputStream("src/main/resources/credential.properties")) {

			Properties prop = new Properties();

			// load a properties file
			prop.load(input);

			// get the property value and print it out
			username = CryptoUtil.decrypt(prop.getProperty("username"));
			password = CryptoUtil.decrypt(prop.getProperty("password"));

		} catch (IOException ex) {
			ex.printStackTrace();
		}
	}

	/**
	 * Uploads file to the job portal
	 * 
	 * @param resume - absolute path to the resume file to be uploaded, it can be
	 *               pdf/docx
	 */
	public static void upload(String resume) {
		if (!enable) {
			driver = new EdgeDriver();
			//driver.manage().window().maximize();
		}
		try {
			// Login
			driver.get(hardcodedURLs.get("login"));
			delay(1);

			WebElement username = driver.findElement(By.id("usernameField"));
			WebElement password = driver.findElement(By.id("passwordField"));

			username.sendKeys(Resume.username);
			password.sendKeys(Resume.password);

			WebElement login = driver.findElement(By.xpath("//*[@id=\"loginForm\"]/div[2]/div[3]/div/button[1]"));

			login.click();
			delay(1);

			// Profile
			driver.get(hardcodedURLs.get("profile"));
			delay(2);

			WebElement uploadElement = driver.findElement(By.id("attachCV"));

			uploadElement.sendKeys(resume);
			delay(4);

			// Logout
			driver.get(hardcodedURLs.get("logout"));
			System.out.println("Exit..");
			delay(1);
		} catch (Exception e) {
			e.printStackTrace();
		}

		if (!enable) {
			driver.close();
			driver.quit();
		}
	}

	private static void delay(int k) {
		System.out.println("wait " + k + " secs");
		try {
			Thread.sleep(k * 1000);
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
	}

	public static void main(String[] args) {

		String resume = "C:\\Users\\manoranjan.kumar\\Downloads\\vc\\Manoranjan_Resume.pdf";
		upload(resume);
	}
}


package com.naukri.profile_update;

import java.util.Timer;
import java.util.TimerTask;

public class Scheduler {

	public static void main(String[] args) throws InterruptedException {

		Timer timer = new Timer();
		TimerTask task = new MyTask();
		timer.schedule(task, 5000, 12000);
	}
}

class MyTask extends TimerTask {

	private String resume = "C:\\Users\\manoranjan.kumar\\Downloads\\vc\\Manoranjan_Resume.pdf";

	@Override
	public void run() {
		Resume.upload(resume);
	}
}

```
