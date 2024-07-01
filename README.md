# Phoenix
A project that I did during my internship at 19. Here you can find only its readme and some screenshots. Source code is provided on demand

## About the project
This is a webapp for the Phoenix project. Its second version. We took only some elements from the previous version developed by several interns, the rest was created from zero. The main reasons for the development of the new app version were that:
* V1 had several bugs
* It was developed by 6 interns that led to the lack of cohesion
* The code looked like spaghetti, it was not easy to understand and maintain
* Models and some methods lacked efficiency

If you need more information about the Phoenix itself, you can find it [here](https://man.s19.be/view/pedago/phoenix/).

## Team
* Aleksandr Buzdin ([abuzdin](https://profile.intra.42.fr/users/abuzdin) / [medved](https://profile.intra.42.fr/users/medved)) - most of frontend, half of views, the first versions of models and condition checks, readme, migration method
* Benjamin Perraudin ([bperraud](https://profile.intra.42.fr/users/bperraud) / [nymano](https://profile.intra.42.fr/users/nymano)) - refactoring, models and checks update and optimization, the other half of views, utils, forms, tasks, the first versions of html templates for forms, db population methods, some frontend (navbar!), git comparison

## Models
While designing the models, we aimed at reducing the amount of data stored in the database. Currently the project has four models in the database:
* ***BlackListUser*** - holds information about users who cannot use Phoenix
* ***PhoenixUser*** - stores vital information about the user and its project. For every week a new PhoenixUser is created
* ***PhoenixWeek*** - represents a time period (currently one week), during which participants are supposed to fullfill the requirements in order to stay in the programme
* ***Requirement*** - contains requirements for a user to stay in Phoenix programme
* ***ByPass*** - a model that allows to bypass a certain requirements. It is required to manages situations when a participant cannot be present at school and work on its project

## Pages
### User pages
Students has access only to the index page, where they see either their Phoenix progress (if they are registered for the programme) or an info message

### Staff pages
* *Index* - displays the current PhoenixWeek. If you add `?login=[USER_LOGIN]` to the url, you can see the user's view for the current week
* *Add* - allows to:
  - Add a new *PhoenixUser*
  - Add *ByPass* to a certain *PhoenixUser*
  - Edit requirements
  - Blacklist a *User*
* *Status* - lists *PhoenixUsers* with different statuses
* *History* - contains some statistics on the *PhoenixUsers* and history for every *PhoenixWeek*
* *User page* - accessible by clicking on a *PhoenixUser* profile picture. It holds information about the *User* and its personal Phoenix history (all *PhoenixUsers* and *PhoenixWeeks*)
* *Blacklist* - lists all blacklisted users. Can remove a user from this page
* *Search* - makes it possible to apply a login filter on a certain page. Mainly useful on *Gaming* page

## Requirements

### To enter
* Have never failed the Phoenix before
* Have no more than 4 weeks before the black hole
* No level limitation?
* No project limitation?

### To validate
* Login days (blocking) - the number of days a student should be present at school during a phoenix week - MIN_VALUE: 4 days in total
* Login hours (blocking) - student's logtime during a phoenix week - MIN_VALUE: 25 hours in total
* Slots (blocking) - the amount of correction slots a student is required to put - MIN_VALUE: 2 hours (8 slots) per day, 3 slot days in total; slots are counted only if a student was present at school
* Exam (blocking) - exam attendance - active only if there is an exam event at the student's campus; otherwise always true
* Correction (blocking) - the phoenix's project correction - only one review is mandatory; after it is done, a user should give up the project; full defense is considered as a slot day; correction is counted from Tuesday till Tuesday
* Improvement (non blocking, checked by staff) - the final mark for the current week should be better than two previous grades

### Requirements change
* We have the initial values for the requirements
* if a requirement is modified, its delta from the initial value is stored (instead of the new value). Like git changes or blockchain operations

### Bypass
* To add a bypass, you need to select a user and set bypass duration
* For every day of justified absence, a user has to do -5 hours, -1 slot and login days (only if the current requirement for slot and login days is more than 1)
* For 5 and more days of justified absence, the requirement for the current week are set to 0

## Management (DB population)
* To populate [MODEL_NAME], execute inside the docker container: `./manage.py populate_reborn populate [MODEL_NAME]`
* To populate all: `./manage.py populate_reborn populate all`
* To migrate old data (normally you don't need it): `./manage.py migrate_data [FILE_PATH]`

## Notes
* If a phoenix_user hasn't chosen a project for Phoenix, the system will do this itself. On every load of any page with conditions progress assessment, there is a check that looks for the last correction a) done by phoenix_user b)during phoenix_week and c) on the project from the phoenix_user's circle

## Sources
* [Icons](https://icon-sets.iconify.design/)
* [Docs](https://htmx.org/docs/) on htmx

## Screenshots
![alt text](https://github.com/baltsaros/fractol/blob/main/pics/1.jpeg)