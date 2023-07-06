# Test Repo for Laravel Nova

I found a performance issue while upgrading a customers Laravel Nova installation from
version 2 to 4.

## The issue

Link: https://github.com/laravel/nova-issues/issues/5690

Our customer has ~60.000 records in users table. Using a filter on colum `email`
reduces the performance a lot. In earlier version 2 opening the filter needs less than 300ms
and opening the email selectbox costs less than a second. After upgrading to Nova 4 opening
the filterbox needs 12 seconds and opening the email selectbox costs ~24 seconds while
browser interrupts you with questions to close the tab or still waiting until process may end.

## How to reproduce

Clone this repository: https://github.com/sfroemkenjw/nova-test-performance

It contains an DDEV environment. So start the project with: `ddev start`

The database needs to be migrated: `ddev artisan migrate`

Create an admin user: `ddev artisan nova:user`

Launch PhpMyAdmin: `ddev launch -p`

Select database `db` and import the file: `./db-import-for-table-users.sql`
It just contains records since ID 2. So your admin will not be deleted.
Big thanks to the service of: https://filldb.info/

Visit user resources in admin area of nova:
https://nova-test-performance.ddev.site/nova/resources/user-resources

Click on the filter icon and wait...and wait...wait ;-)
