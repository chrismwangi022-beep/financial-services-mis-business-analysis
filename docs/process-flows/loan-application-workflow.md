# Loan Application Workflow — As-Is Process Documentation

## 1. Document Information

| Attribute | Details |
|---|---|
| Document ID | BA-PROC-001 |
| Process Name | Loan Application |
| Business Domain | Financial Services / Lending Operations |
| Analysis Type | As-Is Process Analysis |
| Status | Initial documentation based on available observations and notes |
| Evidence Basis | Previously documented user-interface walkthrough |
| Validation Status | Further system behavior requires verification |

## 2. Purpose

Document the observed user-facing workflow for initiating and saving a loan application in the Spread Capital Management Information System (MIS).

The document provides a structured description of the process, its actors, inputs, sequence of activities, potential exceptions, and outstanding validation questions.

## 3. Scope

### In Scope

- Accessing the Apply Loan function.
- Searching for an existing customer.
- Selecting the matching customer record.
- Opening the loan application form.
- Entering loan details from manually completed loan forms supplied by branches.
- Completing required fields.
- Initiating the save action.

### Out of Scope

- Loan eligibility calculations and scoring logic.
- Credit approval or sanctioning rules.
- Backend processing and database behavior.
- Integration with external systems.
- Automatic notifications or downstream processing.
- Final loan approval and disbursement.

These activities are outside this workflow's verified scope.

## 4. Process Participants

| Participant | Responsibility |
|---|---|
| MIS User | Searches for the customer, opens the application form, enters loan details, and initiates saving. |
| Branch / Loan Officer | Supplies the manually completed loan application information used by the MIS user. |

The exact system roles, permissions, and formal responsibility assignments have not been independently verified.

## 5. Preconditions

1. The user can access the MIS and the Apply Loan function.
2. The loan application information has been supplied through the relevant manual loan form.
3. The customer can be searched using an available identifier, such as an ID number or phone number.

The existence and enforcement of additional preconditions require validation.

## 6. Primary Workflow Sequence

| Step | Actor | Action | Expected / Observable Outcome |
|---|---|---|---|
| 1 | MIS User | Navigates to Apply Loan in the sidebar. | The loan application search interface is displayed. |
| 2 | MIS User | Enters the customer's ID number or phone number into the search field. | The user initiates a customer search. |
| 3 | MIS User | Reviews the available search result(s) and identifies the intended customer, where a matching record is returned. | The system displays the available search result(s), if any, for the user to review. |
| 4 | MIS User | Selects Apply Loan for the matching customer. | The loan application form is displayed. |
| 5 | MIS User | Enters the loan details using the manual loan form supplied by the branch. | The application fields are populated with the supplied information. |
| 6 | MIS User | Completes the fields indicated as required by the interface. | The user has entered the information requested by the visible form. |
| 7 | MIS User | Where applicable, uses the Fee Schedule Estimate function. | A fee-estimate function is available; the resulting calculation, validation, and system behavior are not verified. |
| 8 | MIS User | Reviews the entered information and initiates the Save Loan action. | A save request is initiated. The final save outcome remains unverified. |

**Important:** The final step describes the user's action, not proof that the application is successfully saved. Confirmation messages, generated application references, persistence, and subsequent workflow transitions have not been verified.

## 7. Alternative and Exception Scenarios

The following are proposed scenarios for investigation, not confirmed system behaviors.

| ID | Scenario | Expected Behavior to Validate |
|---|---|---|
| ALT-001 | No customer matches the search criteria. | Determine how the system communicates that no matching customer was found and what actions remain available. |
| ALT-002 | Multiple customer records match the search. | Determine how the user identifies the correct customer and prevents selection of the wrong record. |
| ALT-003 | The user leaves a required field empty. | Determine whether the system prevents saving and identifies the missing field. |
| ALT-004 | The user enters data in an invalid format. | Determine whether field-level validation occurs and how errors are communicated. |
| ALT-005 | The user initiates Save Loan but the operation fails. | Determine whether an error is displayed and whether the entered data is retained. |
| ALT-006 | The user initiates saving more than once. | Determine whether duplicate applications can be created or whether duplicate-submission controls exist. |
| ALT-007 | The user attempts to leave the form with unsaved changes. | Determine whether changes are discarded, retained, or subject to a confirmation prompt. |

## 8. Preliminary Business Rules and Constraints

The following statements are limited to the information available from the documented walkthrough.

| ID | Statement | Classification |
|---|---|---|
| BR-001 | The user searches for an existing customer before initiating the loan application. | Observed workflow sequence |
| BR-002 | The customer search accepts an ID number or phone number as a search input. | Previously observed interface workflow |
| BR-003 | Loan details are entered using information supplied through manual loan forms from branches. | Documented operational input |
| BR-004 | The interface indicates fields that the user must complete. | Previously observed interface behavior |
| BR-005 | A Save Loan action is available to initiate saving. | Previously observed interface behavior |

These statements do not establish the underlying validation logic, mandatory-field enforcement, duplicate controls, approval requirements, or persistence behavior.

## 9. Open Questions

| ID | Question | Why It Matters |
|---|---|---|
| OQ-001 | What message or state is displayed when no customer is found? | Defines the search exception and user recovery path. |
| OQ-002 | How does the user distinguish between customers with similar details? | Helps prevent incorrect customer selection. |
| OQ-003 | Which loan form fields are mandatory, and are any conditionally required? | Supports accurate requirements and test coverage. |
| OQ-004 | Are loan details validated against business rules before saving? | Establishes the boundary between interface validation and business validation. |
| OQ-005 | What visible confirmation indicates that a loan application has been saved? | Establishes the observable completion criterion. |
| OQ-006 | Is an application reference generated after saving? | Helps identify and trace an application. |
| OQ-007 | What happens when saving fails or the connection is interrupted? | Supports exception handling and data-integrity analysis. |
| OQ-008 | What permissions or subsequent approvals apply after saving? | Clarifies the next workflow stage without assuming it. |

## 10. Preliminary Acceptance Criteria

These criteria describe what should be demonstrated during authorized validation. They are not recorded test results.

- AC-001: An authorized user can navigate to the Apply Loan function.
- AC-002: The user can search for a customer using a supported identifier.
- AC-003: The user can identify and select the intended customer record.
- AC-004: The selected customer's loan application form is displayed.
- AC-005: The user can enter the loan details supplied by the branch.
- AC-006: The interface clearly identifies required fields.
- AC-007: The user can initiate the Save Loan action.
- AC-008: The system provides an observable and unambiguous outcome after the save attempt.
- AC-009: Validation errors and failed save attempts are handled in a way that can be documented and tested.

## 11. Risks and Control Considerations

The following are potential risks to assess, not confirmed incidents or defects.

- Incorrect customer selection may associate an application with the wrong record.
- Manual transcription may introduce differences between the source loan form and the entered data.
- Unclear required-field validation may allow incomplete information to reach later workflow stages.
- An ambiguous save outcome may cause users to retry unnecessarily or be uncertain whether an application exists.
- Unclear failure handling may create uncertainty about data retention and duplicate submissions.

Potential controls should be recommended only after the current system behavior and business requirements have been established.

## 12. Evidence and Traceability

| Evidence ID | Description | Status |
|---|---|---|
| EV-001 | Previously collected notes describing the Apply Loan navigation and customer search. | Available in prior discovery work; source artifact to be linked. |
| EV-002 | Previously collected notes describing the loan form, required fields, and Save Loan action. | Available in prior discovery work; source artifact to be linked. |

No new screenshots, test results, or stakeholder approvals are claimed by this document.

## 13. Next Steps

1. Review the workflow description for accuracy against the existing discovery notes.
2. Link the original authorized evidence where available.
3. Separate confirmed business rules from items requiring stakeholder clarification.
4. Convert the open questions into requirements elicitation questions.
5. Develop test cases for the proposed acceptance criteria.
6. Record actual outcomes only after authorized testing.

---

**Document ID:** BA-PROC-001
**Document Type:** As-Is Process Documentation
**Version:** 0.2
**Status:** Draft — Pending Review and Validation