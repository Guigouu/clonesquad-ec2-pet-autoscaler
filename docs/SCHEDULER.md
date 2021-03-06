
# Event Scheduler

CloneSquad has an integrated time scheduling module leveraging, behing the scene, CloudWatch Event rules.
Each item of the DynamoDB table *'CloneSquad-{GroupName}-Scheduler'* will be translated in a CloudWatch Event rule.

Actions linked to an event are configuration parameter settings in the *'CloneSquad-{GroupName}-Configuration'* DynamoDB table.

An example of a "complex" scaling using the Event scheduler in located in [examples/environments/demo-scheduled-events/](../examples/environments/demo-scheduled-events/). It implements a schedule plan over 2 hours that starts and stops instances to draw a Sinus wave on the Cloudwatch dashboard.

Configuration of an event in the DynamoDB table has the following format: The Key is a uniq name and value is a [MetaString](CONFIGURATION_REFERENCE.md#MetaString).

	| Key            | Value                                                                    |
	|----------------|--------------------------------------------------------------------------|
	| <event_name1>  | cron(0 * * * ? *),config.active_parameter_set=test-pset                  |
	| <event_name2>  | cron(0 6\\,18 0 * ? *),ec2.schedule.min_instance_count=3,ec2.other_key=4 |

Note: Coma needs to be double-escaped with backslashes.



