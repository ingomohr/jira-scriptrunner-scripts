# jira-scriptrunner-scripts
Scriptrunner scripts for Jira (Server)


## Set Custom Field 'Epic Status' to 'Done'
```Groovy
import com.atlassian.jira.component.ComponentAccessor
import com.atlassian.jira.issue.customfields.manager.OptionsManager

// Name of the custom field to change
final customFieldName = "Epic Status"

// New value for that field
final newValue = "Done" // "To Do" is initial value

def optionsManager = ComponentAccessor.getComponent(OptionsManager)
def customFieldManager = ComponentAccessor.customFieldManager
def customField = customFieldManager.getCustomFieldObjects(issue).find { it.name == customFieldName }
def fieldConfig = customField.getRelevantConfig(issue)
def option = optionsManager.getOptions(fieldConfig).getOptionForValue(newValue, null)

assert customField: "Could not find custom field with name $customFieldName"

issue.setCustomFieldValue(customField, option)
```
