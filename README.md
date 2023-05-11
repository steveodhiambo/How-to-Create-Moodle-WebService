![Moodle Logo](https://img.icons8.com/color/144/000000/moodle.png")

# Moodle Webservice Creation

1. Login as admin/manager account.
1. Click on `Site administration tab` -> `Advanced features` then check/set to true `Enable web services`.
1. Click on `Plugins` tab -> `Web services` -> `Manage protocols` then check/set to true `REST protocol` then save changes.
1. Still on `Plugins` tab -> `Web services` -> `External services` -> `Custom Services` -> Add.
1. Set `Name`, `Short name`, `Enabled` = true, `Authorised users only` = true then Add service.
1. Click `Add functions` and set required functions. (Refer to Moodle Documentation for function names)
    - For this project:
        > `core_course_get_courses`, `core_course_get_courses_by_field` ,`core_user_create_users`,`enrol_manual_enrol_users`,`moodle/cohort:assign`, `moodle/cohort:view`, `moodle/category:viewhiddencategories`, `moodle/user:viewdetails`, `moodle/user:viewhiddendetails`, `moodle/course:useremail`, `moodle/user:update`, `enrol/manual:unenrol`
    - Submit `Add functions`.
1. Create a role for the user of this web service.
    - Assign `Short name`, `Custom full name` and `Context`=`System & User`.
    - On `Allow role assignments` select `Student`. NB: REQUIRED for the web service user to assign users the `Student` role during course enrolment.
    - On the `Capability` section `Allow` the following capabilities:
        - webservice/rest:use
        - Any other capabilities required by the web service functions. For this project:
            - > `moodle/course:view`, `moodle/course:update`, `moodle/course:viewhiddencourses`
            - > `moodle/user:create`
            - > `enrol/manual:enrol`, `moodle/role:assign`
    - Submit `Create this role`
1. Create the web service user.
    - Set `Username`, `Authentication method`=`Manual accounts`, `Password` and other required fields.
    - Submit `Create user`.
1. Add the user created above to the role you just created for the web service.
    - Go to `Users` -> `Permissions` -> `Assign system roles` and click on the created role.
    - Add your user to the `Existing users` list.
    - Go back to list and confirm your user has the role.
1. Add user to the service`s`Authorised users` list.
    - Go to `Plugins` -> `Web services` -> `External services`.
    - Find your service and click `Authorised users`
    - Add your user to `Authorised users` list
1. Create a token for your user
    - Go to `Plugins` -> `Web services` -> `Manage tokens` then `Add`.
    - Set `User`, `Service` and the rest as you wish.
    - Save changes.
1. Done
    - Update config in /config/index.php with your user and web service details.
    - Run test.php and ensure you get the token that Moodle has assigned to you as response.
