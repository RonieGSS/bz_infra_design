# Continuous Integration and Continuous Delivery


## Gitflow(CI/CD) Design
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

## Updating SQL Database Table Column

<p>The following diagram demonstrates how to change the column name <em>surname</em> to <em>lastname</em> in the Users table of <b>Job Seeker Database</b>:</p>

<a href="../img/update_sql_column.png" target="_blank">
  <img src="../img/update_sql_column.png" alt="Updating SQL Column">
</a>

<p>As best practice, only additive changes should applied to the database even when modifying columns. The old column can be deleted once the code/application's behaviour with regards to the change is fully tested; which is probably after the next sprint.</p>