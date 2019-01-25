# Copy Custom Image to New Region

```text
az extension add --name image-copy-extension
az image copy --source-resource-group pcc-ocp-images --source-object-name rhel75base --target-location centralus --target-resource-group cus-vm-images-rg --target-name rhel75base --cleanup
```

