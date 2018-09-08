@@ -0,0 +1,137 @@
//******************************************************************************
//
/*
Copyright (c) 2016 Appium Committers. All rights reserved.
 Licensed to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0 
 Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
*/
//
//******************************************************************************
 using System;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using OpenQA.Selenium.Remote;
 namespace CalculatorTest
{
    [TestClass]
    public class BasicScenarios
    {
        protected const string WindowsApplicationDriverUrl = "http://127.0.0.1:4723/wd/hub";
        protected static RemoteWebDriver CalculatorSession;
        protected static RemoteWebElement CalculatorResult;
        protected static string OriginalCalculatorMode;
         [ClassInitialize]
        public static void Setup(TestContext context)
        {
            // Launch the calculator app
            DesiredCapabilities appCapabilities = new DesiredCapabilities();
            appCapabilities.SetCapability("app", "Microsoft.WindowsCalculator_8wekyb3d8bbwe!App");
            appCapabilities.SetCapability("platformName", "Windows");
            appCapabilities.SetCapability("deviceName", "WindowsPC");
            CalculatorSession = new RemoteWebDriver(new Uri(WindowsApplicationDriverUrl), appCapabilities);
            Assert.IsNotNull(CalculatorSession);
            CalculatorSession.Manage().Timeouts().ImplicitlyWait(TimeSpan.FromSeconds(2));
             // Make sure we're in standard mode
            CalculatorSession.FindElementByXPath("//Button[starts-with(@Name, \"Menu\")]").Click();
            OriginalCalculatorMode = CalculatorSession.FindElementByXPath("//List[@AutomationId=\"FlyoutNav\"]//ListItem[@IsSelected=\"True\"]").Text;
            CalculatorSession.FindElementByXPath("//ListItem[@Name=\"Standard Calculator\"]").Click();
             // Use series of operation to locate the calculator result text element as a workaround
            // We currently cannot query element by automationId without using modified appium dot net driver
            // TODO: Use a proper appium/webdriver nuget package that allow us to query based on automationId
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Clear\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Seven\"]").Click();
            CalculatorResult = CalculatorSession.FindElementByName("Display is  7 ") as RemoteWebElement;
            Assert.IsNotNull(CalculatorResult);
        }
         [ClassCleanup]
        public static void TearDown()
        {
            // Restore original mode before closing down
            CalculatorSession.FindElementByXPath("//Button[starts-with(@Name, \"Menu\")]").Click();
            CalculatorSession.FindElementByXPath("//ListItem[@Name=\"" + OriginalCalculatorMode + "\"]").Click();
             CalculatorResult = null;
            CalculatorSession.Dispose();
            CalculatorSession = null;
        }
         [TestInitialize]
        public void Clear()
        {
            CalculatorSession.FindElementByName("Clear").Click();
            Assert.AreEqual("Display is  0 ", CalculatorResult.Text);
        }
         [TestMethod]
        public void Addition()
        {
            CalculatorSession.FindElementByName("One").Click();
            CalculatorSession.FindElementByName("Plus").Click();
            CalculatorSession.FindElementByName("Seven").Click();
            CalculatorSession.FindElementByName("Equals").Click();
            Assert.AreEqual("Display is  8 ", CalculatorResult.Text);
        }
         [TestMethod]
        public void Combination()
        {
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Seven\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Multiply by\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Nine\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Plus\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"One\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Equals\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Divide by\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Eight\"]").Click();
            CalculatorSession.FindElementByXPath("//Button[@Name=\"Equals\"]").Click();
            Assert.AreEqual("Display is  8 ", CalculatorResult.Text);
        }
         [TestMethod]
        public void Division()
        {
            CalculatorSession.FindElementByName("Eight").Click();
            CalculatorSession.FindElementByName("Eight").Click();
            CalculatorSession.FindElementByName("Divide by").Click();
            CalculatorSession.FindElementByName("One").Click();
            CalculatorSession.FindElementByName("One").Click();
            CalculatorSession.FindElementByName("Equals").Click();
            Assert.AreEqual("Display is  8 ", CalculatorResult.Text);
        }
         [TestMethod]
        public void Multiplication()
        {
            CalculatorSession.FindElementByName("Nine").Click();
            CalculatorSession.FindElementByName("Multiply by").Click();
            CalculatorSession.FindElementByName("Nine").Click();
            CalculatorSession.FindElementByName("Equals").Click();
            Assert.AreEqual("Display is  81 ", CalculatorResult.Text);
        }
         [TestMethod]
        public void Subtraction()
        {
            CalculatorSession.FindElementByName("Nine").Click();
            CalculatorSession.FindElementByName("Minus").Click();
            CalculatorSession.FindElementByName("One").Click();
            CalculatorSession.FindElementByName("Equals").Click();
            Assert.AreEqual("Display is  8 ", CalculatorResult.Text);
        }
    }
}
  
92  sample-code/examples/C#/CalculatorTest/CalculatorTest.csproj
@@ -0,0 +1,92 @@
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="14.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
    <ProjectGuid>{B2C5ADFF-D6B5-48C1-BB8C-571BFD583D7F}</ProjectGuid>
    <OutputType>Library</OutputType>
    <AppDesignerFolder>Properties</AppDesignerFolder>
    <RootNamespace>CalculatorTest</RootNamespace>
    <AssemblyName>CalculatorTest</AssemblyName>
    <TargetFrameworkVersion>v4.5</TargetFrameworkVersion>
    <FileAlignment>512</FileAlignment>
    <ProjectTypeGuids>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
    <VisualStudioVersion Condition="'$(VisualStudioVersion)' == ''">10.0</VisualStudioVersion>
    <VSToolsPath Condition="'$(VSToolsPath)' == ''">$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v$(VisualStudioVersion)</VSToolsPath>
    <ReferencePath>$(ProgramFiles)\Common Files\microsoft shared\VSTT\$(VisualStudioVersion)\UITestExtensionPackages</ReferencePath>
    <IsCodedUITest>False</IsCodedUITest>
    <TestProjectType>UnitTest</TestProjectType>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <Optimize>false</Optimize>
    <OutputPath>bin\Debug\</OutputPath>
    <DefineConstants>DEBUG;TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
    <DebugType>pdbonly</DebugType>
    <Optimize>true</Optimize>
    <OutputPath>bin\Release\</OutputPath>
    <DefineConstants>TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
  </PropertyGroup>
  <ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Drawing" />
    <Reference Include="WebDriver, Version=2.52.0.0, Culture=neutral, processorArchitecture=MSIL">
      <HintPath>packages\Selenium.WebDriver.2.52.0\lib\net40\WebDriver.dll</HintPath>
      <Private>True</Private>
    </Reference>
  </ItemGroup>
  <Choose>
    <When Condition="('$(VisualStudioVersion)' == '10.0' or '$(VisualStudioVersion)' == '') and '$(TargetFrameworkVersion)' == 'v3.5'">
      <ItemGroup>
        <Reference Include="Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=10.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL" />
      </ItemGroup>
    </When>
    <Otherwise>
      <ItemGroup>
        <Reference Include="Microsoft.VisualStudio.QualityTools.UnitTestFramework" />
      </ItemGroup>
    </Otherwise>
  </Choose>
  <ItemGroup>
    <Compile Include="BasicScenarios.cs" />
    <Compile Include="Properties\AssemblyInfo.cs" />
  </ItemGroup>
  <ItemGroup>
    <None Include="app.config" />
    <None Include="packages.config" />
  </ItemGroup>
  <Choose>
    <When Condition="'$(VisualStudioVersion)' == '10.0' And '$(IsCodedUITest)' == 'True'">
      <ItemGroup>
        <Reference Include="Microsoft.VisualStudio.QualityTools.CodedUITestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <Private>False</Private>
        </Reference>
        <Reference Include="Microsoft.VisualStudio.TestTools.UITest.Common, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <Private>False</Private>
        </Reference>
        <Reference Include="Microsoft.VisualStudio.TestTools.UITest.Extension, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <Private>False</Private>
        </Reference>
        <Reference Include="Microsoft.VisualStudio.TestTools.UITesting, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <Private>False</Private>
        </Reference>
      </ItemGroup>
    </When>
  </Choose>
  <Import Project="$(VSToolsPath)\TeamTest\Microsoft.TestTools.targets" Condition="Exists('$(VSToolsPath)\TeamTest\Microsoft.TestTools.targets')" />
  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
  <!-- To modify your build process, add your task inside one of the targets below and uncomment it. 
       Other similar extension points exist, see Microsoft.Common.targets.
  <Target Name="BeforeBuild">
  </Target>
  <Target Name="AfterBuild">
  </Target>
  -->
</Project> 
  
22  sample-code/examples/C#/CalculatorTest/CalculatorTest.sln
@@ -0,0 +1,22 @@
﻿
Microsoft Visual Studio Solution File, Format Version 12.00
# Visual Studio 14
VisualStudioVersion = 14.0.23107.0
MinimumVisualStudioVersion = 10.0.40219.1
Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "CalculatorTest", "CalculatorTest.csproj", "{B2C5ADFF-D6B5-48C1-BB8C-571BFD583D7F}"
EndProject
Global
	GlobalSection(SolutionConfigurationPlatforms) = preSolution
		Debug|Any CPU = Debug|Any CPU
		Release|Any CPU = Release|Any CPU
	EndGlobalSection
	GlobalSection(ProjectConfigurationPlatforms) = postSolution
		{B2C5ADFF-D6B5-48C1-BB8C-571BFD583D7F}.Debug|Any CPU.ActiveCfg = Debug|Any CPU
		{B2C5ADFF-D6B5-48C1-BB8C-571BFD583D7F}.Debug|Any CPU.Build.0 = Debug|Any CPU
		{B2C5ADFF-D6B5-48C1-BB8C-571BFD583D7F}.Release|Any CPU.ActiveCfg = Release|Any CPU
		{B2C5ADFF-D6B5-48C1-BB8C-571BFD583D7F}.Release|Any CPU.Build.0 = Release|Any CPU
	EndGlobalSection
	GlobalSection(SolutionProperties) = preSolution
		HideSolutionNode = FALSE
	EndGlobalSection
EndGlobal
  
56  sample-code/examples/C#/CalculatorTest/Properties/AssemblyInfo.cs
@@ -0,0 +1,56 @@
//******************************************************************************
//
/*
Copyright (c) 2016 Appium Committers. All rights reserved.
 Licensed to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0 
 Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
*/
//
//******************************************************************************
 using System.Reflection;
using System.Runtime.CompilerServices;
using System.Runtime.InteropServices;
 // General Information about an assembly is controlled through the following 
// set of attributes. Change these attribute values to modify the information
// associated with an assembly.
[assembly: AssemblyTitle("CalculatorTest")]
[assembly: AssemblyDescription("")]
[assembly: AssemblyConfiguration("")]
[assembly: AssemblyCompany("")]
[assembly: AssemblyProduct("CalculatorTest")]
[assembly: AssemblyCopyright("Copyright © 2016 Microsoft Corporation")]
[assembly: AssemblyTrademark("")]
[assembly: AssemblyCulture("")]
 // Setting ComVisible to false makes the types in this assembly not visible 
// to COM components.  If you need to access a type in this assembly from 
// COM, set the ComVisible attribute to true on that type.
[assembly: ComVisible(false)]
 // The following GUID is for the ID of the typelib if this project is exposed to COM
[assembly: Guid("b2c5adff-d6b5-48c1-bb8c-571bfd583d7f")]
 // Version information for an assembly consists of the following four values:
//
//      Major Version
//      Minor Version 
//      Build Number
//      Revision
//
// You can specify all the values or you can default the Build and Revision Numbers 
// by using the '*' as shown below:
// [assembly: AssemblyVersion("1.0.*")]
[assembly: AssemblyVersion("1.0.0.0")]
[assembly: AssemblyFileVersion("1.0.0.0")]
  
11  sample-code/examples/C#/CalculatorTest/app.config
@@ -0,0 +1,11 @@
﻿<?xml version="1.0" encoding="utf-8"?>
<configuration>
  <runtime>
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
      <dependentAssembly>
        <assemblyIdentity name="Newtonsoft.Json" publicKeyToken="30ad4fe6b2a6aeed" culture="neutral" />
        <bindingRedirect oldVersion="0.0.0.0-8.0.0.0" newVersion="8.0.0.0" />
      </dependentAssembly>
    </assemblyBinding>
  </runtime>
</configuration> 
  
4  sample-code/examples/C#/CalculatorTest/packages.config
@@ -0,0 +1,4 @@
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Selenium.WebDriver" version="2.52.0" targetFramework="net45" />
</packages> 
  
29  sample-code/examples/java/Windows/pom.xml
@@ -0,0 +1,29 @@
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
     <groupId>CalculatorTest</groupId>
    <artifactId>CalculatorTest</artifactId>
    <version>1.0-SNAPSHOT</version>
     <dependencies>
        <dependency>
            <groupId>org.seleniumhq.selenium</groupId>
            <artifactId>selenium-java</artifactId>
            <version>2.53.0</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.11</version>
        </dependency>
        <dependency>
            <groupId>io.appium</groupId>
            <artifactId>java-client</artifactId>
            <version>3.4.1</version>
        </dependency>
    </dependencies>
 </project> 
  
133  sample-code/examples/java/Windows/src/test/java/CalculatorTest.java
@@ -0,0 +1,133 @@
//******************************************************************************
//
//
/*
Copyright (c) 2016 Appium Committers. All rights reserved.
 
Licensed to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0 
 Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
*/
//
//******************************************************************************
 import org.junit.*;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.openqa.selenium.remote.DesiredCapabilities;
import java.util.concurrent.TimeUnit;
import java.net.URL;
import io.appium.java_client.ios.IOSDriver;
import org.openqa.selenium.remote.RemoteWebDriver;
 public class CalculatorTest {
     private static RemoteWebDriver CalculatorSession = null;
    private static WebElement CalculatorResult = null;
     @BeforeClass
    public static void setup() {
        try {
            DesiredCapabilities capabilities = new DesiredCapabilities();
            capabilities.setCapability("app", "Microsoft.WindowsCalculator_8wekyb3d8bbwe!App");
            capabilities.setCapability("platformName", "Windows");
            capabilities.setCapability("deviceName", "WindowsPC");
            CalculatorSession = new RemoteWebDriver(new URL("http://127.0.0.1:4723/wd/hub"), capabilities);
            CalculatorSession.manage().timeouts().implicitlyWait(2, TimeUnit.SECONDS);
             CalculatorSession.findElementByXPath("//Button[starts-with(@Name, \"Menu\")]").click();
            CalculatorSession.findElementByXPath("//ListItem[@Name=\"Standard Calculator\"]").click();
             CalculatorSession.findElementByName("Clear").click();
            CalculatorSession.findElementByName("Seven").click();
            CalculatorResult = CalculatorSession.findElementByName("Display is  7 ");
            Assert.assertNotNull(CalculatorResult);
         }catch(Exception e){
            e.printStackTrace();
        } finally {
        }
    }
     @Before
    public void Clear()
    {
        CalculatorSession.findElementByName("Clear").click();
        Assert.assertEquals("Display is  0 ", CalculatorResult.getText());
    }
     @AfterClass
    public static void TearDown()
    {
        CalculatorResult = null;
        if (CalculatorSession != null) {
            CalculatorSession.quit();
        }
        CalculatorSession = null;
    }
     @Test
    public void Addition()
    {
        CalculatorSession.findElementByName("One").click();
        CalculatorSession.findElementByName("Plus").click();
        CalculatorSession.findElementByName("Seven").click();
        CalculatorSession.findElementByName("Equals").click();
        Assert.assertEquals("Display is  8 ", CalculatorResult.getText());
    }
     @Test
    public void Combination()
    {
        CalculatorSession.findElementByName("Seven").click();
        CalculatorSession.findElementByName("Multiply by").click();
        CalculatorSession.findElementByName("Nine").click();
        CalculatorSession.findElementByName("Plus").click();
        CalculatorSession.findElementByName("One").click();
        CalculatorSession.findElementByName("Equals").click();
        CalculatorSession.findElementByName("Divide by").click();
        CalculatorSession.findElementByName("Eight").click();
        CalculatorSession.findElementByName("Equals").click();
        Assert.assertEquals("Display is  8 ", CalculatorResult.getText());
    }
     @Test
    public void Division()
    {
        CalculatorSession.findElementByName("Eight").click();
        CalculatorSession.findElementByName("Eight").click();
        CalculatorSession.findElementByName("Divide by").click();
        CalculatorSession.findElementByName("One").click();
        CalculatorSession.findElementByName("One").click();
        CalculatorSession.findElementByName("Equals").click();
        Assert.assertEquals("Display is  8 ", CalculatorResult.getText());
    }
     @Test
    public void Multiplication()
    {
        CalculatorSession.findElementByName("Nine").click();
        CalculatorSession.findElementByName("Multiply by").click();
        CalculatorSession.findElementByName("Nine").click();
        CalculatorSession.findElementByName("Equals").click();
        Assert.assertEquals("Display is  81 ", CalculatorResult.getText());
    }
     @Test
    public void Subtraction()
    {
        CalculatorSession.findElementByName("Nine").click();
        CalculatorSession.findElementByName("Minus").click();
        CalculatorSession.findElementByName("One").click();
        CalculatorSession.findElementByName("Equals").click();
        Assert.assertEquals("Display is  8 ", CalculatorResult.getText());
    }
}
  
106  sample-code/examples/python/windows_calculatortest.py
@@ -0,0 +1,106 @@
"""
//******************************************************************************
 Copyright (c) 2016 Appium Committers. All rights reserved.
 Licensed to you under the Apache License, Version 2.0 (the
"License"); you may not use this file except in compliance
with the License.  You may obtain a copy of the License at
http://www.apache.org/licenses/LICENSE-2.0 
 Unless required by applicable law or agreed to in writing,
software distributed under the License is distributed on an
"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
KIND, either express or implied.  See the License for the
specific language governing permissions and limitations
under the License.
 //******************************************************************************
"""
 import unittest
from appium import webdriver
 class SimpleCalculatorTests(unittest.TestCase):
     def setUp(self):
        #set up appium
        desired_caps = {}  
        desired_caps["app"] = "Microsoft.WindowsCalculator_8wekyb3d8bbwe!App"
        desired_caps["platformName"] = "Windows"
        desired_caps["deviceName"] = "WindowsPC"
        self.driver = webdriver.Remote(
            command_executor='http://127.0.0.1:4723/wd/hub',
            desired_capabilities= desired_caps)
     def tearDown(self):
        self.driver.quit()
     def test_initialize(self):
        #Make sure we're in standard mode
        self.driver.find_element_by_xpath("//Button[starts-with(@Name, \"Menu\")]").click();
        self.driver.find_element_by_xpath("//ListItem[@Name=\"Standard Calculator\"]").click();
         self.driver.find_element_by_name("Clear").click()
        self.driver.find_element_by_name("Seven").click()
         result = self.driver.find_element_by_accessibility_id("CalculatorResults")
        self.assertEqual(str(result.text),"Display is  7 ")
     def test_addition(self):
        self.driver.find_element_by_name("One").click()
        self.driver.find_element_by_name("Plus").click()
        self.driver.find_element_by_name("Seven").click()
        self.driver.find_element_by_name("Equals").click()
         result = self.driver.find_element_by_accessibility_id("CalculatorResults")
        self.assertEqual(str(result.text), "Display is  8 ")
     def test_combination(self):
        self.driver.find_element_by_name("Seven").click()
        self.driver.find_element_by_name("Multiply by").click()
        self.driver.find_element_by_name("Nine").click()
        self.driver.find_element_by_name("Plus").click()
        self.driver.find_element_by_name("One").click()
        self.driver.find_element_by_name("Equals").click()
        self.driver.find_element_by_name("Divide by").click()
        self.driver.find_element_by_name("Eight").click()
        self.driver.find_element_by_name("Equals").click()
         result = self.driver.find_element_by_accessibility_id("CalculatorResults")
        self.assertEqual(str(result.text), "Display is  8 ")
     def test_division(self):
        self.driver.find_element_by_name("Eight").click()
        self.driver.find_element_by_name("Eight").click()
        self.driver.find_element_by_name("Divide by").click()
        self.driver.find_element_by_name("One").click()
        self.driver.find_element_by_name("One").click()
        self.driver.find_element_by_name("Equals").click()
        
        result = self.driver.find_element_by_accessibility_id("CalculatorResults")
        self.assertEqual(str(result.text), "Display is  8 ")
     def test_multiplication(self):
        self.driver.find_element_by_name("Nine").click()
        self.driver.find_element_by_name("Multiply by").click()
        self.driver.find_element_by_name("Nine").click()
        self.driver.find_element_by_name("Equals").click()
         result = self.driver.find_element_by_accessibility_id("CalculatorResults")
        self.assertEqual(str(result.text), "Display is  81 ")
     def test_subtraction(self):
        self.driver.find_element_by_name("Nine").click()
        self.driver.find_element_by_name("Minus").click()
        self.driver.find_element_by_name("One").click()
        self.driver.find_element_by_name("Equals").click()
         result = self.driver.find_element_by_accessibility_id("CalculatorResults")
        self.assertEqual(str(result.text), "Display is  8 ")
 if __name__ == '__main__':
    suite = unittest.TestLoader().loadTestsFromTestCase(SimpleCalculatorTests)
    unittest.TextTestRunner(verbosity=2).run(suite) 
  
65  sample-code/examples/ruby/windows_CalculatorTest.rb
@@ -0,0 +1,65 @@
# ******************************************************************************
#
# Copyright (c) 2016 Appium Committers. All rights reserved.
#
#Licensed to you under the Apache License, Version 2.0 (the
#"License"); you may not use this file except in compliance
#with the License.  You may obtain a copy of the License at
#http://www.apache.org/licenses/LICENSE-2.0 
#
#Unless required by applicable law or agreed to in writing,
#software distributed under the License is distributed on an
#"AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#KIND, either express or implied.  See the License for the
#specific language governing permissions and limitations
#under the License.
#
#
#******************************************************************************
require 'selenium-webdriver'
require "test/unit"
 $CalculatorSession
$CalculatorResult
 class CalculatorTest < Test::Unit::TestCase
    def caps 
        {
            platformName: "WINDOWS", platform: "WINDOWS", deviceName: "mydevice", app: "Microsoft.WindowsCalculator_8wekyb3d8bbwe!App" 
        }
    end
     def assert &block
        raise AssertionError unless yield
    end
     def setup
        $CalculatorSession = Selenium::WebDriver.for(:remote, :url => "http://127.0.0.1:4723/wd/hub", :desired_capabilities => caps )
        
        $CalculatorSession.find_elements(:xpath, "//Button[starts-with(@Name, \"Menu\")]")[0].click;
        $CalculatorSession.find_elements(:xpath, "//ListItem[@Name=\"Standard Calculator\"]")[0].click;
         $CalculatorSession.find_elements(:name, "Clear")[0].click;
        $CalculatorSession.find_elements(:name, "Seven")[0].click;
        $CalculatorResult = $CalculatorSession.find_elements(:name, "Display is  7 ")[0];
        assert{$CalculatorResult != nil}
        $CalculatorSession.find_elements(:name, "Clear")[0].click;
    end
     def test_combination
        $CalculatorSession.find_elements(:name, "Seven")[0].click;
        $CalculatorSession.find_elements(:name, "Multiply by")[0].click;
        $CalculatorSession.find_elements(:name, "Nine")[0].click;
        $CalculatorSession.find_elements(:name, "Plus")[0].click;
        $CalculatorSession.find_elements(:name, "One")[0].click;
        $CalculatorSession.find_elements(:name, "Equals")[0].click;
        $CalculatorSession.find_elements(:name, "Divide by")[0].click;
        $CalculatorSession.find_elements(:name, "Eight")[0].click;
        $CalculatorSession.find_elements(:name, "Equals")[0].click;
        assert{$CalculatorResult.text == "Display is  8 "};
    end
     def teardown
        $CalculatorSession.quit
    end
end
