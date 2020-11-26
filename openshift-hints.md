# Various usefull commands:

Delete all not running pods:

oc delete pod --field-selector=status.phase!=Running
