## Version 1.12.0

Compatibility: requires minimum Kimai 2.17.0

- Fixed: booking vacation on "half-day" public holidays wasn't possible
- Fixed: raise max vacation days from 20 to 30
- Fixed: approved timesheets can be deleted
- Fixed: edit dialog for approved timesheets can be opened
- Added: new configuration to disable timesheet booking on non-working days
- Added: new permission `workdays_override_timesheet` to skip the above validation, e.g. for admins

## Version 1.11.0

Compatibility: requires minimum Kimai 2.17.0

- Added: new API methods to fetch public holidays
- Removed: public holidays from Absence API 
- Fixed: showing own absences in other users calendar
- Fixed: use new `hours_other_profile` permission from core 

## Version 1.10.0

Compatibility: requires minimum Kimai 2.12.0

- Changed: support attribute caching in Voter
- Fixed: permission check for PDF download
- Fixed: public holidays in calendar missing

## Version 1.9.0

Compatibility: requires minimum Kimai 2.12.0

- Added: system configuration to set absence comment-field optional
- Added: allow to assign half days for user contract "holidays per year"
- Added: allow to use half days in "manual bookings"
- Added: allow to set duration for "sickness" 
- Added: auto-approve all open days of the year before the lock date
- Changed: single line comment field for "manual bookings" form 
- Fixed: use correct base class for migration - removes Doctrine deprecation warning

## Version 1.8.0

Compatibility: requires minimum Kimai 2.11.0

- Added: absence types have a color
- Added: use type colors on absence screen and for calendar entries
- Fixed: translate calendar entries in current locale, instead of absence users locale
- Fixed: do not show error on calendar if `absences` permission is deactivated for a user
- Changed: use refactored language vs locale from user for email generation

## Version 1.7.0

Compatibility: requires minimum Kimai 2.10.0

- Added: send notification email to supervisor for new absences
- Added: cross-link absence and work-contract page
- Added: trigger event when absences are created
- Fixed: editing absences could show fields (like "half day" for sickness) that should not be there 

## Version 1.6.0

Compatibility: requires minimum Kimai 2.9.0

- Fixed: export of absences caused 500
- Changed: replaced DateTime with DateTimeInterface / DateTimeImmutable

## Version 1.5.0

Compatibility: requires minimum Kimai 2.8.0

- Added: new category to book "unpaid holiday" absences
- Added: generic calculation logic to prevent required adjustments for new categories
- Added: different duration limitation for absence types (e.g. 75 days in one booking for parental leave)
- Added: command `bin/console kimai:bundles:workcontract:absence-types` to debug absence types
- Fixed: time calculation for new "child is sick" and "parental leave" categories
- Fixed: deprecation by using DateTimeImmutable

## Version 1.4.0

Compatibility: requires minimum Kimai 2.7.0

- Added: manual adjustments for holidays, e.g. top up available days with remaining days from last year
- Added: added category to book "child is sick" absences
- Added: added category to book "parental leave" absences
- Added: prevent booking absences across a time-range of two years
- Added: limit selectable time-range to selected year
- Fixed: day calculation of vacations with public holidays in between 

## Version 1.3.0

Compatibility: requires minimum Kimai 2.5.0

- Fixed: adapted collapsible boxes for Kimai 2.5.0
- Fixed: allow booking holidays with public holidays within the selected date-range

## Version 1.2.0

Compatibility: requires minimum Kimai 2.1.0

- Fixed: some users could not see public holidays in the calendar
- Fixed: route mapping type changed to attribute
- Fixed: Homepage link in extension screen

## Version 1.1.0

Compatibility: requires minimum Kimai 2.0.34

- Added: data migration from MR plugins
- Added: show absences in calendar
- Added: show public-holidays in calendar
- Added: export absences to excel
- Fix: possible pagination issue
