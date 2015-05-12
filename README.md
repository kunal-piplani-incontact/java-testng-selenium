testng-selenium
======================
> Remove the TestNG Selenium boilerplate.

<h2 id="overviewSection">Overview</h2>
<ol>
  <li><a href="#overviewSection">Overview</a></li>
  <li><a href="#projectGoalsSection">Project Goals</a></li>
  <li><a href="#mavenDependencySection">Maven Dependency</a></li>
  <li><a href="#writingSuitesSection">Writing Suites</a></li>
  <li><a href="#writingAPageFactorySection">Writing a Page Factory</a></li>
  <li><a href="#writingAPageObjectSection">Writing a Page Object</a></li>
  <li><a href="#configuringSection">Configuring</a>
    <ul>
      <li><a href="#systemBasedConfigurationSection">System Based Configuration</a></li>
      <li><a href="#annotationBasedConfigurationSection">Annotation Based Configuration</a></li>
    </ul></li>
</ol>
<h2 id="projectGoalsSection">Project Goals</h2>
<ul>
  <li>Configuration through System properties and annotations.</li>
  <li>Facilitate running tests in parallel.</li>
  <li>Remove typical boilerplate, such as taking screenshots on test
    failures, configuring WebDriver, and instantiating page objects.</li>
  <li>Declarative way of defining page objects with PageFactory.</li>
  <li>Declarative way of configuring tests individually.</li>
</ul>
<h2 id="mavenDependencySection">Maven Dependency</h2>
<script src="https://gist.github.com/jsdevel/9b3638c9a10472234e73.js"></script>
<h2 id="writingSuitesSection">Writing Suites</h2>
In each of your suite classes, extend <code>AbstractSuite</code> and pass
  your PageFactory as a generic type argument.
<br/>
<br/>
<script src="https://gist.github.com/jsdevel/a1b0bd45673077b997e4.js"></script>
<br/>
<code>AbstractSuite</code> provides a <code>getPageFactory</code>
method to create the page factories passed in as generic type arguments.  In
this example, the page factory passed as a generic type on line 7 is
returned by <code>getPageFactory</code>.
<h2 id="writingAPageFactorySection">Writing a Page Factory</h2>
A PageFactory is nothing more than an interface:
<br/>
<br/>
<script src="https://gist.github.com/jsdevel/ccf7b410397f3e59fddb.js"></script>
<br/>
Each method declared in a <code>PageFactory</code> should return a sub class
of <code>AbstractPage</code>.  This allows TestNG-Selenium to do some cool things
when initializing your page objects, like navigating to them when
<code>WebDriver</code> has been created, wiring up annotated fields using
Selenium's PageFactory initializer, and validating that the URL currently
being viewed by WebDriver is valid for the requested page.  This approach
also allows you to avoid boilerplate by letting TestNG-Selenium manage your
page factory's lifecycle.
<h2 id="writingAPageObjectSection">Writing a Page object.</h2>
<ol>
  <li>Create a class I.E. GoogleHomePage</li>
  <li>Extend com.github.jsdevel.testng.selenium.AbstractPage.</li>
  <li>Pass your page object's type, and the page factory used to create it
    as generic type arguments to AbstractPage.</li>
  <li>Optionally add WebElement fields annotated with @FindBy (see
    <a href='https://code.google.com/p/selenium/wiki/PageFactory'>Google's
      PageFactory pattern.</a>).</li>
</ol>
<script src="https://gist.github.com/jsdevel/c9936738506d22e03722.js"></script>
If you need to do something before validation occurs, such as wait for
requests, or poll a global javascript variable, you can override
<code>AbstractPage#handlePageInitialized()</code>.
<h2 id="configuringSection">Configuring</h2>
TestNG-Selenium may be configured in one of 2 ways:
<ul>
  <li>System Properties</li>
  <li>Annotations</li>
</ul>
In general, annotation based configuration overrides system based
configuration on a per test basis.
<h3 id="systemBasedConfigurationSection">System Based Configuration</h3>
Here is a list of the system properties recognized by TestNG-Selenium with their default values:
<br/>
<br/>
<script src="https://gist.github.com/jsdevel/481a97b58d534e325824.js"></script> 
<h3 id="annotationBasedConfigurationSection">Annotation Based Configuration</h3>
Here is an example of how we can override a system property using an annotation
for a single test run.  For the full list of supported annotations, see
package contents under com.github.jsdevel.annotations.
<br/>
<br/>
<script src="https://gist.github.com/jsdevel/95035a9b12925e6711ae.js"></script> 
