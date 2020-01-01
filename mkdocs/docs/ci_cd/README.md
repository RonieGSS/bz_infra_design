# Continuous Integration and Continuous Delivery


## Gitflow(CI/CD) Design

<p>The following diagram demonstrates implementation of zero-downtime deployment using Rolling Update Strategy with Kubernetes:</p>

<a href="../img/ci_cd.png" target="_blank">
  <img src="../img/ci_cd.png" alt="Continuous Integration and Delivery">
</a>

<p>The matching services will be deployed on a kubernetes cluster.</p>
<p>However, for Introduction Service Features the static assets will be built in Build Stage of CI/CD and will be deployed to S3 (probably using S3cmd command).</p>
<p>The above diagram shows three environments with respective git branches to run deployments:</p>
<ul>
	<li>Development (development branch)</li>
	<li>Stage (staging branch)</li>
	<li>Production (master or release branch which is recommended for version tagging purposes)</li>
</ul>

<p>The three environments/git branch will have up to four CI/CD stages:</p>
<ul>
	<li>Source Stage - fetches all the source code from the repository triggered by a developer pushing to any of the above branches</li>
	<li>Build Stage - this stage is where assets are compiled and docker images are built and sent to ECR (container registry in AWS)</li>
	<li>Test Stage - this stage is where unit and static analysis tests for development and user acceptance and integration tests for staging are executed</li>
	<li>Deploy Stage -  this stage is where assets are sent to s3, docker image is deployed to kubernetes, and database migration if necessary is executed</li>
</ul>
<p>When any of the above stages failed, the developer(s) must recreate a new branch to fix the issue. Creating a new ticket for this issue depending on type is also recommended.</p>

## Updating SQL Database Table Column

<p>The following diagram demonstrates how to change the column name <em>surname</em> to <em>lastname</em> in the Users table of <b>Job Seeker Database</b>:</p>

<a href="../img/update_sql_column.png" target="_blank">
  <img src="../img/update_sql_column.png" alt="Updating SQL Column">
</a>

<p>As best practice, only additive changes should applied to the database even when modifying columns. The old column can be deleted once the code/application's behaviour with regards to the change is fully tested; which is probably after the next sprint. Such practice is to ensure zero-downtime deployment.</p>