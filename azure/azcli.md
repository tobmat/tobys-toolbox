##### Update template on resource group

az group update -n '{{ resourceGroupName }}' --set tags.environment='{{ environmentTag }}'



