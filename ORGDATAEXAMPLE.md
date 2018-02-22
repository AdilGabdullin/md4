# Org Data Required Fields
Must be included in upload file

|Attribute<br>(Names must match, case sensitive)|Description|Data Coverage Requirements|Format Examples|
|-----------------------------------------------|-----------|--------------------------|---------------|
|PersonId|Unique identifier for the employee record. Recommend the primary SMTP is used. Can be email address, alias, or UPN for the employee, must be in simplified format (such as: person.name@xyz.com, not <Name, Person> (person.name@xyz.com)).<br>NOTE: This is hidden in the query output row level data|Each row must contain a valid PersonId.<br>Each load file can have only ONE record with the same PersonID / EffectiveDate pair.|person.name@xyz.com|
|EffectiveDate|Date for which the given attribute value applies for the employee, of the form MM/DD/YYYY. The attribute will apply until another record for the same attribute with a different effective date is specified.  The first effective date must be more than 13 months prior to the processing date.|Each row must contain a valid EffectiveDate.<br>Each load file can have only ONE record with the same PersonID / EffectiveDate pair.|MM/DD/YYYY|
|HireDate|Date the employee began employment. This date determines the beginning date for calculating metrics of a measured employee. If an employee has multiple hire dates (for example: first hire date, most recent hire date), we recommend using the most recent hire date.|Each row should ideally contain a valid HireDate.<br>If not included, metrics will be calculated from the start date of the data collection period.|MM/DD/YYYY|
|ManagerId|Unique identifier for the employee’s manager. Can be email address, alias, or UPN and must be in simplified format. This data is needed to correctly calculate metrics for time spent with managers and their direct reports. NOTE: This is hidden in the query output row level data|Each row must contain a value.  If no manager, can use something like “nomanager@xyz.com”|manager.name@xyz.com|
|TimeZone|Time zone the employee does work in. This must be one of the Windows nomenclature time zones. If you do not have time zone available for each employee, the system will use the default provided.|Each row should contain a value. If not present, the default will be used.|Pacific Standard Time|
|LevelDesignation|The employee’s level, represented as a string. The level can represent an employee’s experience or management level, or seniority within the organization, and will be specific to your organization. This data is needed to correctly calculate metrics for redundancy and insularity.|Each row must contain a value.  If no value exists for an employee, can use a dummy term such as “not applicable”|CEO, Vice President, Director, Manager, IC|
|Organization|The internal organization the employee belongs to. An employee’s organization will be specific to your individual needs and could be identified by the leader of the organization, or other naming convention. This data is needed to correctly calculate metrics for redundancy and insularity.  Important to choose the right level based on how you want to group, filter, or compare your data.|Each row must contain a value.  If no value exists for an employee, can use a dummy term such as “not applicable”|Marketing, Finance, Johnson, Jones, Roberts…|

# Org Data Reserved Fields
If included, must meet the specific criteria and naming conventions outlined below

|Attribute<br>(Names must match, case sensitive)|Description|Data Coverage Requirements|Format Example|
|-----------------------------------------------|-----------|--------------------------|--------------|
|FunctionType|The job function the employee performs. This is also specific to your organization. This data is used to filter and group reports, and for grouping of data in Explore metrics features.|This column header is not required to be present; if it is present, then all rows must contain a value.  If there is no value for an employee, use a dummy value such as “not applicable”.|Software Engineering, Program Management, Finance Management|
|Layer|The place in the organizational hierarchy that the employee belongs, represented as an integer and expressed as distance from the CEO, who is at layer 0. This data is used to filter and group reports, and for grouping of data in Explore metrics features.|This column header is not required to be present; if it is present, then all rows must contain a value.  If there is no value for an employee, use a dummy value such as “not applicable”.|0,1,2,3,…|
|HourlyRate|The salary of the employee, represented as an hourly rate (if you have annual rate, divide each record by 2080). The value can be expressed as pay only, or loaded including full value of benefits; only requirement is that it is consistently specified across all employees. This is not yet used in calculations but can be used to filter and group employees. Note that the Explore metrics feature uses a default HourlyRate of $75 that currently cannot be changed.|This attribute column header is not required to be present; if it is present, then all rows must contain a floating point or integer value.  **DO NOT INCLUDE A “$” SIGN**|75|

# Org Data Common Additional Fields
Note: Avoid special characters

|Attribute|Description|Format Example|Potential Specific Use Cases|
|---------|-----------|--------------|----------------------------|
|Location|Location of the employee.  Often this is broken up into multiple fields to represent different levels of detail (Country, Region, State, City).  For workspace planning cases, you may go to the site or building level.|United States<br>West Region<br>Washington<br>Seattle|All<br>More specific attributes for Workspace Planning|
|Organization2|Drill down of Organization to get to a more specific group of employees. An employee’s organization will be specific to your individual needs and could be identified by the leader of the organization, or other naming convention.|HR Talent Management|All|
|Organization3|(see description above for Organization2)|Learning and Development|All|
|Cost Center|Cost center groupings of employees|Center A, Center B…|All|
|RoleType|An indicator of whether the role is an Individual Contributor, Manager, or Manager of Managers|IC, Mgr, Mgr+|All|
|EmployeeType|An indicator of whether the employee is a contractor, vendor, exempt, non-exempt, or other employee type designations|Vendor, Regular, etc|All|
|Tenure|Length of tenure at the company|6|All|
|Title|Standard Job Title|Sr Software Engineer|All|
|Performance Rating|Employee performance rating category.  This can be useful in looking at work patterns of high performing people.|Exceeds, Meets, Does not Meet|All|
|EngagementScore|Employee engagement score rating category.  This can be useful in looking at work patterns associated with engaged employees.|High, Medium, Low|Employee Engagement<br>Manager Effectiveness|
|QuotaAttainment|Employee quota attainment category.  This can be useful in looking at work patterns associated with high performing sales roles.|Exceeds, Meets, Does not Meet|Sales Productivity|
|ManagerScore|Manager feedback survey score rating categories.  This can be useful in looking at manager effectiveness initiatives.|High, Medium, Low|Employee Engagement<br>Manager Effectiveness|
