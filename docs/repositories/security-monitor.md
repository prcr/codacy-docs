# Quality Security Monitor

{%
    include-markdown "../assets/includes/paid.md"
    start="<!--paid-start-->"
    end="<!--paid-end-->"
%}

The **Quality Security Monitor** provides an overview of all security issues that Codacy found on your repository, and also warns you if any security code patterns are currently turned off.

!!! tip
    For an organization-level overview of security vulnerabilities, use the [Security and Risk Management](../organizations/managing-security-and-risk.md) dashboard instead.

By default, the page displays the overview for the main branch of your repository but if you have [more than one branch enabled](../repositories-configure/managing-branches.md) you can use the drop-down list at the top of the page to display information for other branches.

![Security Monitor](images/security-monitor.png)

The left-hand side of the dashboard lists the status for each security category that the tools that can analyze the programming languages in your repository support:

<style>
/* Center text in the first column */
#status th:first-child, #status td:first-child {
  text-align: center !important;
}
</style>

<table id="status">
  <thead>
    <tr>
      <th>Status</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><img src="../images/security-monitor-red.png" alt="Red"></td>
      <td><strong>Codacy found security issues in this category</strong><br/><br/>
          Click the category name to see the list of security issues in this category, and click the title of the issues to see more information about the issue.<br/><br/>
          This status takes precedence over the yellow status, meaning that some code patterns in the category may be turned off. Fix the existing security issues or use the <a href="../../repositories-configure/configuring-code-patterns/"><strong>Code patterns</strong> page</a> to check if there are any code patterns turned off in this category.</td>
    </tr>
    <tr>
      <td rowspan="2"><img src="../images/security-monitor-yellow.png" alt="Yellow"></td>
      <td><strong>There are security code patterns in this category that are turned off</strong><br/><br/>
          You should turn on the code patterns in this category so that Codacy can find the corresponding security issues. Click the category name to see the code patterns that are turned off, and click the check box next to each code pattern to turn it on.<br/><br/>
          To turn on all security code patterns on the repository regardless of their category, click the button <strong>More</strong> and select <strong>Turn on all security patterns</strong>.</td>
    </tr>
    <tr>
      <td style="display: none;"></td>
      <td><strong>Codacy can't determine if all security code patterns in this category are turned on or not</strong><br/><br/>
          This happens when you use configuration files to control which code patterns are turned on, when the tool is disabled, or when it's a <a href="../../repositories-configure/local-analysis/client-side-tools/">client-side tool</a>. Ensure that you manually turn on the listed code patterns in your configuration files, that the tool is enabled, and check if the tool runs client-side.</td>
    </tr>
    <tr>
      <td><img src="../images/security-monitor-green.png" alt="Green"></td>
      <td><strong>Everything is OK for this category</strong><br/><br/>
          All security code patterns in this category are turned on, and Codacy didn't find security issues in this category.</td>
    </tr>
  </tbody>
</table>

!!! tip
    You can use the **Warnings** drop-down list to display only security categories that have found issues or categories that have code patterns turned off.

## Languages checked for security issues

The Security Monitor supports checking the languages and frameworks below for any security issues reported by the corresponding tools:

<!--NOTE
    When adding a new supported tool, make sure that you update the following pages:

    docs/getting-started/supported-languages-and-tools.md
    docs/repositories-configure/local-analysis/client-side-tools.md (if the tool runs client-side)
    docs/repositories/security-monitor.md (if the tool reports security issues)
    docs/repositories-configure/configuring-code-patterns.md (supported configuration files table, or list of tools that don't support configuration files)
    docs/repositories-configure/codacy-configuration-file.md (list of tool short names to use on the Codacy configuration file)
-->

<table>
  <thead>
    <tr>
      <th>Language or framework</th>
      <th>Tools that report security issues</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Apex</td>
      <td><a href="https://pmd.github.io/">PMD</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a></td>
    </tr>
    <tr>
      <td>AWS CloudFormation</td>
      <td><a href="https://github.com/bridgecrewio/checkov/">Checkov</a>,
          <a href="https://trivy.dev">Trivy</a> <a href="#yaml-only"><sup>2</sup></a></td>
    </tr>
    <tr>
      <td>C</td>
      <td><a href="https://clang.llvm.org/extra/clang-tidy/">Clang-Tidy</a><a href="#client-side"> <sup>3</sup></a>,
          <a href="http://cppcheck.sourceforge.net/">Cppcheck</a>,
          <a href="https://dwheeler.com/flawfinder/">Flawfinder</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>C#</td>
      <td><a href="https://github.com/SonarSource/sonar-dotnet">SonarC#</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>C++</td>
      <td><a href="https://clang.llvm.org/extra/clang-tidy/">Clang-Tidy</a><a href="#client-side"> <sup>3</sup></a>,
          <a href="http://cppcheck.sourceforge.net/">Cppcheck</a>,
          <a href="https://dwheeler.com/flawfinder/">Flawfinder</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Dart</td>
      <td><a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Dockerfile</td>
      <td><a href="https://github.com/hadolint/hadolint">Hadolint</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Elixir</td>
      <td><a href="https://github.com/rrrene/credo">Credo</a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Go</td>
      <td><a href="https://github.com/securego/gosec">Gosec</a><a href="#client-side"> <sup>3</sup></a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Groovy</td>
      <td><a href="https://codenarc.github.io/CodeNarc/">CodeNarc</a></td>
    </tr>
    <tr>
      <td>Helm</td>
      <td><a href="https://trivy.dev">Trivy</a> <a href="#yaml-only"><sup>2</sup></a></td>
    </tr>
    <tr>
      <td>Java</td>
      <td><a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://spotbugs.github.io/">SpotBugs</a><a href="#client-side"> <sup>3</sup></a><a href="#spotbugs-plugin"> <sup>4</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>JavaScript</td>
      <td><a href="https://eslint.org/">ESLint</a> <a href="#eslint-plugin"><sup>5</sup></a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>JSON</td>
      <td><a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Kotlin</td>
      <td><a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a></td>
    </tr>
    <tr>
      <td>Kubernetes</td>
      <td><a href="https://trivy.dev">Trivy</a> <a href="#yaml-only"><sup>2</sup></a></td>
    </tr>
    <tr>
      <td>Objective-C</td>
      <td><a href="https://clang.llvm.org/extra/clang-tidy/">Clang-Tidy</a><a href="#client-side"> <sup>3</sup></a></td>
    </tr>
    <tr>
      <td>PHP</td>
      <td><a href="https://github.com/squizlabs/PHP_CodeSniffer">PHP_CodeSniffer</a>,
          <a href="https://phpmd.org/">PHP Mess Detector</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>PowerShell</td>
      <td><a href="https://github.com/PowerShell/PSScriptAnalyzer">PSScriptAnalyser</a></td>
    </tr>
    <tr>
      <td>Python</td>
      <td><a href="https://github.com/PyCQA/bandit">Bandit</a>,
          <a href="https://github.com/landscapeio/prospector">Prospector</a>,
          <a href="https://github.com/pylint-dev/pylint">Pylint</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Ruby<a href="#ruby-31"> <sup>6</sup></a></td>
      <td><a href="https://brakemanscanner.org/">Brakeman</a>,
          <a href="https://github.com/rubocop/rubocop">RuboCop</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Rust</td>
      <td><a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Scala</td>
      <td><a href="https://github.com/codacy/codacy-scalameta">Codacy Scalameta Pro</a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://spotbugs.github.io/">SpotBugs</a><a href="#client-side"> <sup>3</sup></a><a href="#spotbugs-plugin"> <sup>4</sup></a></td>
    </tr>
    <tr>
      <td>Swift</td>
      <td><a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a></td>
    </tr>
    <tr>
      <td>Shell</td>
      <td><a href="https://www.shellcheck.net/">ShellCheck</a>
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a></td>
    </tr>
    <tr>
      <td>Terraform</td>
      <td><a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Transact-SQL</td>
      <td><a href="https://github.com/tsqllint/tsqllint/">TSQLLint</a></td>
    </tr>
    <tr>
      <td>TypeScript</td>
      <td><a href="https://eslint.org/">ESLint</a> <a href="#eslint-plugin"><sup>5</sup></a>,
          <a href="https://semgrep.dev/">Semgrep</a> <a href="#semgrep"><sup>1</sup></a>,
          <a href="https://trivy.dev">Trivy</a></td>
    </tr>
    <tr>
      <td>Visual Basic</td>
      <td><a href="https://github.com/SonarSource/sonar-dotnet">SonarVB</a></td>
    </tr>
  </tbody>
</table>

<sup><span id="semgrep">1</span></sup>: Semgrep supports additional security rules when signing up for [Semgrep Pro](https://semgrep.dev/pricing/).  
<sup><span id="yaml-only">2</span></sup>: Currently, Trivy only supports scanning YAML files on this platform.  
<sup><span id="client-side">3</span></sup>: Supported as a [client-side tool](../repositories-configure/local-analysis/client-side-tools.md).  
<sup><span id="spotbugs-plugin">4</span></sup>: Includes the plugin [Find Security Bugs](https://find-sec-bugs.github.io/).  
<sup><span id="eslint-plugin">5</sup>: Includes the shareable config [<span class="skip-vale">nodesecurity</span>](https://www.npmjs.com/package/eslint-config-nodesecurity) and the plugins [angularjs-security-rules](https://www.npmjs.com/package/eslint-plugin-angularjs-security-rules), [no-unsafe-innerhtml](https://www.npmjs.com/package/eslint-plugin-no-unsafe-innerhtml), [no-unsanitized](https://www.npmjs.com/package/eslint-plugin-no-unsanitized), [scanjs-rules](https://www.npmjs.com/package/eslint-plugin-scanjs-rules), [security](https://www.npmjs.com/package/eslint-plugin-security), and [security-node](https://www.npmjs.com/package/eslint-plugin-security-node).  
<sup><span id="ruby-31">6</span></sup>: Currently, Codacy doesn't support any static code analysis tool for [Ruby 3.1](https://www.ruby-lang.org/en/news/2021/12/25/ruby-3-1-0-released/).  

## Supported security categories

Each issue reported on the Security Monitor belongs to one of the following security categories:

<!--NOTE
    Currently, this category doesn't include any security issues
    https://github.com/codacy/codacy-tools/pull/496#discussion_r892437164

|**Firefox OS**|Security issues related to sensitive APIs of Firefox OS.|
-->

|Security category|Description|
|-----------------|-----------|
|**Android**|Android-specific security issues.|
|**Authentication**|Broken authentication and authorization attacks consist in gaining access to accounts that allow disclosing sensitive information or performing operations that could compromise the system.|
|**Command Injection**|Command injection attacks aim to execute arbitrary commands on the host operating system.|
|**Cookies**|Security issues related to insecure cookies.|
|**Cryptography**|Cryptography attacks exploit failures related to cryptography (or lack thereof), <span class="skip-vale">potentially</span> leading to exposure of sensitive data.|
|**CSRF**|Cross-Site Request Forgery (CSRF) attacks force an end user to execute unwanted actions on a web application in which they're currently authenticated.|
|**Denial of Service**|Denial of Service (DoS) attacks make a resource (site, application, server) unavailable for legitimate users, typically by flooding the resource with requests or exploiting a vulnerability to trigger a crash.|
|**File Access**|File access security issues may allow an attacker to access arbitrary files and directories stored on the file system such as application source code, configuration, and critical system files.|
|**HTTP Headers**|Insecure HTTP headers are a common attack vector for malicious users.|
|**Input Validation**|Client input should always be validated to prevent malformed or malicious data from entering the workflow of an information system.|
|**Insecure Modules and Libraries**|Security issues related to modules or libraries that can <span class="skip-vale">potentially</span> include vulnerabilities.|
|**Insecure Storage**|Security issues related to insecure storage of sensitive data.|
|**Malicious Code**|Security issues related to code patterns that are <span class="skip-vale">potentially</span> unsafe.|
|**Mass Assignment**|Unprotected mass assignments are a Rails feature that could allow an attacker to update sensitive model attributes.|
|**Regex**|Regular expressions can be used in Denial of Service attacks, exploiting the fact that in most regular expression implementations the computational load grows exponentially with input size.|
|**Routes**|Badly configured routes can give unintended access to an attacker.|
|**SQL Injection**|SQL injection attacks insert or "inject" malicious SQL queries into the application via the client input data.|
|**SSL**|Security issues related with old SSL versions or configurations that have known cryptographic weaknesses and should no longer be used.|
|**Unexpected Behaviour**|Security issues related to <span class="skip-vale">potentially</span> insecure system API calls.|
|**Visibility**|Logging should always be included for security events to better allow attack detection and help defend against vulnerabilities.|
|**XSS**|Cross-Site Scripting (XSS) attacks inject malicious client-side scripts into trusted websites that are visited by the end users.|
|**Other**|Other language-specific security issues.|

## See also

-   [Issues page](issues.md)
-   [Configuring code patterns](../repositories-configure/configuring-code-patterns.md)
