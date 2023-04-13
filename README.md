# Salesforce Code Analyzer Custom Rules
A repository with custom SFDX code analyzer rules

The rules folder contains individual PMD rules for Salesforce. The test folder contains tests for the PMD rules using the PMD Rule Designer.

## Rules

### Avoid using Test.isRunningTest()

Avoid using Test.isRunningTest() in code since this results in code that cannot be unit tested.

## How to use


To use these rules, create a rule set file and copy the required rules into the rule set file (after the end of the description tag).

For example, create a rule set xml file (`DesignRuleset.xml`) with the following contents:

```xml
<?xml version="1.0"?>
<ruleset name="Design"
    xmlns="http://pmd.sourceforge.net/ruleset/2.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://pmd.sourceforge.net/ruleset/2.0.0 https://pmd.sourceforge.io/ruleset_2_0_0.xsd">
    <description>Design</description>
    <rule name="AvoidTestIsRunningStmts"
        language="apex"
        message="Avoid using Test.isRunningTest()"
        class="net.sourceforge.pmd.lang.rule.XPathRule">
        <description>
            Avoid using Test.isRunningTest() in code since this results
            in code that cannot be unit tested.
    </description>
        <priority>1</priority>
        <properties>
            <property name="version" value="2.0" />
            <property name="xpath">
                <value>
    <![CDATA[
    //MethodCallExpression[lower-case(@FullMethodName) = "test.isrunningtest"]
    ]]>
            </value>
            </property>
        </properties>
    </rule>
</ruleset>
```
The rule set name and description defines the "Category" of the rules.

Store this file in a directory that contains `category`, e.g. `rules/category/apex`

The ruleset can be added to the Salesforce Code Analyzer with the command:
`sfdx scanner:rule:add --language apex --path "rules/category/apex/DesignRuleset.xml"`