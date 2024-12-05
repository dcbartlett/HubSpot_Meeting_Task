## Changes

Hubspot meetings processor was added to `worker.js`

Domain updated to include lastPulledDates for meetings

## Notes

Hubspot meetings do not have the properties requested to be added.  Code accounts for this and skips adding the meeting if the properties are not available.

## Code Changes needed for future itterations.

`server.js` has an express application that has no routes.  This server is not needed in it's current state.  Routes need to be added to this or removed from the project.

The above mentioned server does not continue running because when `worker.js` is complete, it exits the node process.

Migrations should be added to the project to handle updates to the structure of the mongoDB collections.  This will allow the existing collection objects to be conformed to any new schema changes.

The project has some unused variables.  These should be cleaned up.

`saveDomain` is disabled in `worker.js`.  This should be investigated to understand if it needs to be re-enabled.

`worker.js` has many duplicated code blocks.  A refactoring can be done to create a processor factory for which refreshAccessToeken, contacts, companies, and meetings would be passed through.  This will handle the technical logic like circuity breaking while letting the predicates of the factory handle business logic.

During processing of contacts, an API Request call is made to fetch associations.  This can be switched over to useing the `associations.batchApi` class in the `hubspotClient` library.

During logging of errors, apiKeys are being stroed to the log entries.  This should be evaluated and determined if this is a security risk.
