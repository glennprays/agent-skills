# Handoff templates

Send the immediate instruction with the task ID and revision. Include enough approved text to execute if the other agent cannot open the record. Keep optional ideas and discarded alternatives in the director discussion.

## Director to executor

~~~text
Continue <task ID> at <revision> in your existing session.
Source — <task file or the approved direction below>.
Changed since <prior revision> — <criterion or decision delta>.
Next — <specific outcome or evidence to obtain>.
Verification — <criterion IDs, check, and expected behavior>.
Report back with the revision, actual result, and any decision you need.
~~~

For a first handoff or when source access differs, include the task objective, agreed constraints and scope, criteria, and dependencies the executor needs to act. On subsequent handoffs, forward the complete updated decision when a delta alone would be ambiguous.

## Executor to director

~~~text
<task ID> · <revision worked on> · <baseline when relevant>
Completed — <what changed>
Evidence — <criterion, source or check, and actual result>
Open — <fact, blocker, or missed criterion>
Decision needed — <question and consequence>, if applicable
~~~

## Example checkpoint

An executor reports that one 14-day request failed. The active requirement says the default is seven days. Ask the executor to verify whether the response indicates a provider maximum or a malformed request. Keep the active requirement at its existing revision during the check. If the user later approves changing the product's maximum, issue a new revision with the specific criterion delta. Keep earlier test results tied to the version tested.
