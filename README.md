# geicocode
sample selenium learning on geico site

package geico;

import java.util.concurrent.TimeUnit;

import org.openqa.selenium.Alert;
import org.openqa.selenium.By;
import org.openqa.selenium.By.ByXPath;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.firefox.FirefoxDriver;
import org.openqa.selenium.support.ui.ExpectedConditions;
import org.openqa.selenium.support.ui.Select;
import org.openqa.selenium.support.ui.WebDriverWait;


public class geicologin {

	public static void main(String[] args) throws Exception 

	{
		//Initializing Excel Code
		OpenExcel.setExcelFile("D://Selenium//erw.xlsx","Sheet1");

		//Initializing Browser
		WebDriver 	driver=new FirefoxDriver();
		WebDriverWait wait = new WebDriverWait(driver, 10);
		driver.manage().window().maximize();

		//Home Page Validations	 

		driver.get("https://www.geico.com/"); 
		String expectedTitle = "An Insurance Company For Your Car And More | GEICO";
		String actualTitle = driver.getTitle();
		System.out.println(actualTitle);

		if (expectedTitle.equals(actualTitle)) 
		{

			System.out.println("verification successful - The correct Tile is Displayed on the Webpage");
		} 
		else 
		{
			System.out.println("verification unsuccessful");
		}

		driver.findElement(By.xpath(".//*[@id='submitButton']")).click();

		WebDriverWait wait2 = new WebDriverWait(driver, 10);

		//Page 1 - Code


		driver.findElement(By.xpath("//input[@id='CustomerForm:firstName']")).sendKeys(OpenExcel.getCellData(1, 0));

		Thread.sleep(4000);

		driver.findElement(By.xpath("//input[@id='CustomerForm:lastName']")).sendKeys(OpenExcel.getCellData(1, 1));
		driver.findElement(By.xpath("//input[@id='CustomerForm:customerMailingAddress']")).sendKeys(OpenExcel.getCellData(1, 2));
		driver.findElement(By.xpath("//input[@class='unitno']")).sendKeys(OpenExcel.getCellData(1, 3));
		driver.findElement(By.xpath("//input[@name='CustomerForm:mailingZip']")).sendKeys(OpenExcel.getCellData(1, 4));



		WebDriverWait wait4 = new WebDriverWait(driver, 10);

		WebElement element = wait.until(ExpectedConditions.elementToBeClickable(By.xpath(".//*[@id='CustomerForm:mailingCityRowTR']/td[1]/label")));

		Thread.sleep(200);
		String CityState= driver.findElement(By.xpath(".//*[@id='CustomerForm:mailingCityRowTR']/td[1]/label")).getText();

		String ActualCityState= "City, State";

		if (CityState.equals(ActualCityState)) 
		{

			System.out.println("verification successful - City State field is been displayed");
		} 
		else 
		{
			System.out.println("verification unsuccessful - City State field is not displayed ");
		}



		driver.findElement(By.xpath(".//*[@id='CustomerForm:birthMonth']")).sendKeys(OpenExcel.getCellData(1, 5));
		driver.findElement(By.xpath(".//*[@id='CustomerForm:birthDay']")).sendKeys(OpenExcel.getCellData(1, 6));
		driver.findElement(By.xpath(".//*[@id='CustomerForm:birthYear']")).sendKeys(OpenExcel.getCellData(1, 7));

		WebElement R1 = driver.findElement(By.xpath(".//*[@id='CustomerForm:fqUnmarriedDriver:1']"));

		Boolean checkradiobuttonisselected=R1.isSelected();

		if (checkradiobuttonisselected == false) 
		{
			R1.click();
			System.out.println("numberofdriverinforadiobutton is selected");
		} 

		else 
		{
			System.out.println("numberofdriverinforadiobutton is selected by default to no");

		}
		driver.findElement(By.xpath("//input[@class='square']")).click();

		//Page 2 - code

		String Page2Name=driver.findElement(By.xpath("//h1[contains(text(),'Add Vehicle Information')]")).getText();

		System.out.println(Page2Name);

		WebElement make=driver.findElement(By.xpath("//span[@id='VehicleForm:selectBorder2']/select"));

		Boolean checkmakeisdisabled=make.isEnabled();

		if (checkmakeisdisabled == false)
		{
			System.out.println("make drop down is not enabled");
		}

		new Select(driver.findElement(By.xpath("//select[@id='VehicleForm:year']"))).selectByValue("2016");

		WebDriverWait wait7 = new WebDriverWait(driver, 10);
		new Select( wait.until(ExpectedConditions.elementToBeClickable(By.xpath(".//*[@id='VehicleForm:make']")))).selectByValue("A MARTIN");

		WebDriverWait wait8 = new WebDriverWait(driver, 10); 
		new Select(wait.until(ExpectedConditions.elementToBeClickable(By.xpath(".//*[@id='VehicleForm:model']")))).selectByValue("V8 VANTAGE");

		WebDriverWait wait9 = new WebDriverWait(driver, 10); 
		new Select(wait.until(ExpectedConditions.elementToBeClickable(By.xpath(".//*[@id='VehicleForm:bodystyle']")))).selectByVisibleText("Convertible");


		driver.findElement(By.xpath("//input[@id='VehicleForm:hybrid:1']")).click();

		new Select(driver.findElement(By.xpath(".//*[@id='VehicleForm:odometerReading']"))).selectByValue("99");
		new Select(driver.findElement(By.xpath(".//*[@id='VehicleForm:ownership']"))).selectByValue("L");
		new Select(driver.findElement(By.xpath(".//*[@id='VehicleForm:otherBusiness']"))).selectByVisibleText("Pleasure");
		Thread.sleep(2000);

		driver.findElement(By.xpath("//input[@name='VehicleForm:addNo']")).click();

		//new Select(driver.findElement(By.xpath("//select[@id='VehicleForm:estimatedMileage']"))).selectByVisibleText("4,001 - 5,000");

		//Page 3 Code

		new Select(driver.findElement(By.xpath(".//*[@id='DriverForm:maritalStatus']"))).selectByVisibleText("Single"); 

		driver.findElement(By.xpath(".//*[@id='DriverForm:gender:0']")).click();

		new Select(driver.findElement(By.xpath(".//*[@id='DriverForm:curInsComp']"))).selectByVisibleText("Yes"); 

		driver.findElement(By.xpath(".//*[@id='DriverForm:firstUSLicenseAge']")).sendKeys("19");

		driver.findElement(By.xpath(".//*[@id='DriverForm:ageFirstLicensedForeign']")).sendKeys("19");
		Thread.sleep(200);

		driver.findElement(By.xpath(".//*[@id='DriverForm:fulltimeStudent:1']")).click();
		
		WebDriverWait wait10 = new WebDriverWait(driver, 10); 
		new Select(wait.until(ExpectedConditions.elementToBeClickable(By.xpath(".//*[@id='DriverForm:currentYearOfStudy']")))).selectByVisibleText("High School Student");
	

		//new Select(driver.findElement(By.xpath(".//*[@id='DriverForm:currentYearOfStudy']"))).selectByVisibleText("High School Student"); 

		new Select(driver.findElement(By.xpath(".//*[@id='DriverForm:guardReserveRetiree_otherStates']"))).selectByVisibleText("Does Not Apply");

		driver.findElement(By.xpath(".//*[@id='DriverForm:addNo']")).click();
		
		
		// Pag4 Code
		
		driver.findElement(By.xpath(".//*[@id='DriHisForm:select:1']")).click();
		driver.findElement(By.xpath(".//*[@id='DriHisForm:continueBtn']")).click();
		
		//Page 5 Code
		new Select(driver.findElement(By.xpath(".//*[@id='CurrentInsuranceForm:currentBodilyInjury']"))).selectByVisibleText("$15,000/$30,000");
		driver.findElement(By.xpath(".//*[@id='CurrentInsuranceForm:continueBtn']")).click();
		
		//Page 6 Code
		driver.findElement(By.xpath(".//*[@id='DiscountsForm:spnsMkAlumniAssociationsInd']")).click();
		driver.findElement(By.xpath(".//*[@id='DiscountsForm:emailAddress']")).sendKeys(OpenExcel.getCellData(1, 8));
		
		driver.findElement(By.xpath(".//*[@id='eBill1']")).click();
		driver.findElement(By.xpath(".//*[@id='DiscountsForm:continueBtn']")).click();

	}


}




Reading Excel Code:

package geico;


import java.io.*;
import org.apache.poi.xssf.usermodel.*;


public class OpenExcel 
{

       private static XSSFSheet ExcelWSheet;
    
    private static XSSFWorkbook ExcelWBook;

    private static XSSFCell Cell;

    private static XSSFRow Row;
    
    public static void setExcelFile(String Path,String SheetName) throws Exception {
           
                  try {

                  // Open the Excel file

                  FileInputStream ExcelFile = new FileInputStream(Path);

                  // Access the required test data sheet

                  ExcelWBook = new XSSFWorkbook(ExcelFile);

                  ExcelWSheet = ExcelWBook.getSheet(SheetName);

                  } catch (Exception e){

                        throw (e);

                  }

    }
    public static String getCellData(int RowNum, int ColNum) throws Exception{
           
                  try{

                  Cell = ExcelWSheet.getRow(RowNum).getCell(ColNum);

                  String CellData = Cell.getStringCellValue();

                  return CellData;

                  }catch (Exception e){

                        return"";

                  }

}

    
    public static void setCellData(String Result,  int RowNum, int ColNum) throws Exception  {
           
                  try{

                  Row  = ExcelWSheet.getRow(RowNum);

                  Cell = Row.getCell(ColNum);
                  

                  if (Cell == null) {

                        Cell = Row.createCell(ColNum);

                        Cell.setCellValue(Result);

                        } else {

                               Cell.setCellValue(Result);

                        }

// Constant variables Test Data path and Test Data file name

                  //"D://ToolsQA//OnlineStore//src//testData//"
                        FileOutputStream fileOut = new FileOutputStream("D://Selenium//erw.xlsx");

                        ExcelWBook.write(fileOut);

                        fileOut.flush();

                               fileOut.close();

                        }catch(Exception e){

                               throw (e);

                  }

           }

}


