<h1>SQL-PySpark Conversion Agent</h1>
<h2>Agent to convert SQL queries to Standard PySpark Code</h2>

<h2>Problem</h2>
Data engineers commonly receive SQL-based transformation logic from analysts, SMEs, or upstream systems, but Spark pipelines require PySpark DataFrame APIs.
Manual conversion causes complications.
<ol>
  <li>Rewriting SQL queries into PySpark can be time-consuming.</li>
  <li>Human errors in complex queries (JOIN, GROUP BY, HAVING, CASE WHEN).</li>
  <li>Inconsistent coding patterns across team members</li>
  <li>Blockers in large-scale cloud migrations from SQL-based systems to Spark.</li>
</ol>

<h2>Solution</h2>
This project implements an Enterprise AI Agent built using <b>Google ADK</b> and <b>Gemini 2.5 Flash-Lite</b> that:
<ol>
<li>Accepts any SQL query</li>
<li>Normalizes and canonicalizes it</li>
<li>Automatically converts it into PySpark DataFrame code</li>
<li>Handles complex logic such as</li><ul>
   <li>CASE WHEN → F.when().otherwise()</li>
   <li>JOINs</li>
   <li>Aggregations</li>
   <li>Filters & grouping</li></ul>
<li>Validates the generated code via a rule-based evaluation engine</li>
<li>Supports batch test cases for automated QA</li>
</ol>

<h2>Architecture</h2>
         <div align="center">┌─────────────────────┐</div>
        <div align="center">     SQL Input Query    </div>
          <div align="center">└──────────┬──────────┘</div>
            <div align="center">             ▼</div>
           <div align="center">(1) SQL Normalizer Agent</div>
           <div align="center">             ▼</div>
       <div align="center">(2) SQL → PySpark Conversion Agent</div>
                    <div align="center">    ▼</div>
             <div align="center">PySpark Code Output</div>
             <div align="center">           ▼</div>
        <div align="center">(3) Rule-Based Evaluation Engine</div>
          <div align="center">              ▼</div>
         <div align="center">Evaluation Scores + Diagnostics</div>

<h2>Component</h2>
<table>
  <tr>
    <th>Component</th>
    <th>Description</th>
  </tr>
  <tbody>
    <tr>
      <td><b>SQL Normalizer Agent (LLM)</b></td>
      <td>Cleans and standardizes SQL to reduce ambiguity before conversion.</td>
    </tr>
    <tr>
      <td><b>Conversion Agent (LLM)</b></td>
      <td>Converts SQL into PySpark DataFrame operations.</td>
    </tr>
    <tr>
      <td><b>Sequential Agent Pipeline</b></td>
      <td>Ensures ordered execution of Normalizer → Converter.</td>
    </tr>
    <tr>
      <td><b>InMemorySessionService</b></td>
      <td>Maintains state for agent pipeline executions.</td>
    </tr>
    <tr>
      <td><b>Rule-Based Evaluation Engine</b></td>
      <td>Validates correctness without additional LLM calls.</td>
    </tr>
    <tr>
      <td><b>Test Harness</b></td>
      <td>Allows batch evaluation of multiple SQL test cases.</td>
    </tr>
  </tbody>  
</table>

<h2>Essential Tools</h2>
<table>
  <tr>
    <th>Technology</th>
    <th>Purpose</th>
  </tr>
  <tbody>
    <tr>
      <td><b>Google ADK</b></td>
      <td>Build structured agents, pipelines, and stateful runners.</td>
    </tr>
    <tr>
      <td><b>Gemini 2.5 Flash-Lite</b></td>
      <td>Fast, lightweight LLM for conversion logic.</td>
    </tr>
    <tr>
      <td><b>Python</b></td>
      <td>Evaluation, orchestration, and test harnessing.</td>
    </tr>
    <tr>
      <td><b>Rule-Based Evaluation</b></td>
      <td>Ensures correctness without extra compute.</td>
    </tr>
  </tbody>  
</table>

<h2>Setup Instructions</h2>
<h3>1. Install Dependencies</h3>
pip install google-adk google-genai

<h3>2. Set Environment Variables</h3>
<p>import os</p> 
<p>os.environ.setdefault("GOOGLE_GENAI_USE_VERTEXAI", "FALSE")</p>
<p>os.environ["GOOGLE_API_KEY"] = "YOUR_API_KEY"</p>

<h2>Value Statement</h2>
This Agent significantly accelerates data engineering workflows by:
<ol>
  <li>Reducing SQL → PySpark conversion time by up to 90%</li>
  <li>Eliminating human error in complex SQL rewrites</li>
  <li>Standardizing PySpark code across projects</li>
  <li>Improving productivity during cloud migration initiatives</li>
  <li>Allowing analysts with SQL skills to contribute to Spark workloads</li>
</ol>
