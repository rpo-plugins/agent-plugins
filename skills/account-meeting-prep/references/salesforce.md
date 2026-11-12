# Salesforce (ClaudeForce)

Read this when the CRM connector is Salesforce's (ClaudeForce, the
"Salesforce - Beta" connector in Claude).

## The tools

ClaudeForce does not have one tool per object. It has five general tools:

- `discover`: search Salesforce's library of recipes and API operations.
- `describe`: get the steps or the request shape for an id that `discover`
  returned.
- `dispatch_readonly`: run a GET call. **Use only this one in this skill.**
- `dispatch`: run calls that change data. **Never use it in this skill.**
- `display_widget`: draw a Salesforce widget. Not needed for the brief.

Record reads are SOQL queries. Run `discover` once (for example "query
records with SOQL", `resultType: "endpoint"`), then `describe` the query
operation it returns. Then call `dispatch_readonly` with `method: "GET"`, the
query path exactly as `describe` returned it (for example
`/services/data/v66.0/query`), and the SOQL in `queryParams.q`. Pass
`userType: "business"`.

## What to read, for the account in the meeting

Find the account first, then read the rest by its `Id`. One query per object
keeps each result small:

- **Account**: `SELECT Id, Name, Owner.Name FROM Account WHERE Name LIKE
  '%<company>%' LIMIT 10`. Escape any `'` in the name as `\'`. If more than one
  comes back, ask which one, or pick by an exact name match.
- **Opportunities**, open ones first: `Name, StageName, Amount, Probability,
  CloseDate, Owner.Name, IsClosed`, `WHERE AccountId = '<id>'`, ordered by
  `IsClosed, CloseDate`.
- **Contacts** who are attending: `Name, Title, Email`, `WHERE AccountId =
  '<id>'`. Match on the names the user gave.
- **Events**: `Subject, StartDateTime, Description, Who.Name`, `WHERE
  AccountId = '<id>'`, around the meeting date. Descriptions often hold the
  agenda.
- **Tasks**, especially open or overdue ones: `Subject, Status, ActivityDate,
  Description, Owner.Name`, `WHERE AccountId = '<id>'`. These are often the
  customer's explicit asks ("bring two ideas on X").
- **Recent activity and notes** from the last few months: completed Tasks and
  past Events, newest first, with their `Description`.

If a query errors because a field does not exist in this org, drop that field
and run it again; orgs differ.

## Reading what comes back

- **An Amount of 0 or empty usually means nobody has entered one.** Write "no
  amount entered", not "$0".
- **The Amount is what the deal is worth to the seller.** It is not the
  customer's value from r.Potential, and the two never get added together.
- Quote stage names as Salesforce spells them; each org defines its own.

## Matching the account to r.Potential

Salesforce and r.Potential can spell the same company differently. Match by
meaning, not by exact text, and ask when two r.Potential accounts could fit.
A Salesforce account can also be a subsidiary or a regional entity of a company
r.Potential holds as one account; say so in the brief when that happens.

## What not to do

- Do not call `dispatch`, or anything else that writes to Salesforce.
- Do not treat r.Potential's dollar ranges as opportunity amounts or roll them
  into pipeline totals.
