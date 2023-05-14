Saturday 13 May

Summary
At 9:24 PM Pacific Time (PT) the error tracking tool :wqthat we use on the project reported an abrupt spike in errors on the live production server. The issue affected critical functionality of the website, so at 9:28 PM our team switched the website to maintenance mode and it wasn’t available to end users. The root cause of the incident turned out to be a database failure caused by an incorrectly written script. The issue was fully resolved by 10:23 PM and the website was fully functional again.
Timeline
9:23 PM PT − The update of the production database was finished.
9:24 PM PT − Our monitoring tool detected an abrupt spike in errors.
9:26 PM PT − Our team started checking logs to find out what had caused the incident.
9:28 PM PT − We moved the website into maintenance.
9:37 PM PT − We initiated the task that would restore the production database.
9:43 PM PT − We optimized Sidekiq workers to speed up database restoration.
9:55 PM PT − We switched off the maintenance mode; at the time, 80% of all products were listed and only 20% were still missing.
10:23 PM PT − The production database was fully restored and the incident was resolved.
Root case
During a planned update to the production database, a newly added script that worked with its structure turned out to have been written incorrectly. As a result, the script removed a large number of products from the item_datafeed table that contains the URLs that lead to retailers’ online stores.

Resolution and recovery
At 9:24 PM PT our team received lots of alerts from our error tracking software, and we immediately started investigating the issue.

At 9:26 PM PT, we started to check logs and quickly found out that the issue was caused by a production database failure. To minimize customer dissatisfaction, at 9:28 PM PT we decided to move the website into maintenance mode. Afterward, our team initiated the task to restore the production database, and we also optimized Sidekiq workers to speed up database restoration.

When 80% of products in the database had already been restored (at 9:55 PM PT), our team decided to move the website back to production, and at 10:23 PM PT all products were listed on the website and available to customers.
Corrective and preventive measures
Having analyzed the incident in-depth, our team came up with the following measures for preventing similar incidents in future:

Although we rely heavily on tests in our development workflow, we will test even changes related to database updates on the staging server prior to rolling them out on the production server.
We will back up all databases used on the project on a regular basis so that we can roll them back easily in case of incidents. Apart from automated scheduled backups, our team will introduce database backups before all major changes.
We will increase test coverage of the application to ensure that all critical parts of functionality are 100% covered with automated tests.
