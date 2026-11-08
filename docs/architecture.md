# GiveBack architecture

## Request path

The React client calls ASP.NET Core controllers. Commands and queries pass through MediatR to application handlers. Domain entities represent the volunteering workflow. The infrastructure layer supplies EF Core persistence with SQL Server.

The use cases are organized around operations such as publishing opportunities, submitting applications, and logging or verifying hours. Commands and queries have separate handlers while sharing the application’s relational store.

## Relational model

| Record | Relationships in the application |
| --- | --- |
| Opportunity | Belongs to an organization, can be classified by cause, and can have many applications. |
| Application | References an opportunity and associates the application with a volunteer or team. |
| Hour log | References a volunteer and an opportunity, can be associated with an application, and can record the verifying organization. |
| Volunteer team | Holds team membership separately from team applications. |

Keeping applications and time records separate lets the application represent selection and participation as distinct steps. Hour records can be verified without changing the opportunity’s published information. The schema also has separate records for notifications, certificates and impact reports.

This is a conceptual model for the portfolio. It omits personal data, credentials, deployment settings, and operational endpoints.

[Back to GiveBack](../README.md)
