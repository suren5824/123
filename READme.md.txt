{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "certificates_AzureRunAsCertificate_base64Value": {
            "type": "SecureString"
        },
        "automationAccounts_Surendhar_name": {
            "defaultValue": "Surendhar",
            "type": "String"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Automation/automationAccounts",
            "apiVersion": "2015-10-31",
            "name": "[parameters('automationAccounts_Surendhar_name')]",
            "location": "westus",
            "properties": {
                "sku": {
                    "name": "Basic"
                }
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/certificates",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRunAsCertificate')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "description": "This certificate is used to authenticate with the service principal that was automatically created for this account. For details on this service principal and certificate, or to recreate them, go to this account’s Settings. For example usage, see the tutorial runbook in this account.",
                "isExportable": true,
                "thumbprint": "BD0A9A8BE8A16831E86268E1184B7B277D5FBB14",
                "base64Value": "[parameters('certificates_AzureRunAsCertificate_base64Value')]"
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/connections",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRunAsConnection')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "connectionType": {
                    "name": "AzureServicePrincipal"
                }
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/connectionTypes",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Azure')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "isGlobal": true,
                "fieldDefinitions": {
                    "AutomationCertificateName": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    },
                    "SubscriptionID": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    }
                }
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/connectionTypes",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureClassicCertificate')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "isGlobal": true,
                "fieldDefinitions": {
                    "SubscriptionName": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    },
                    "SubscriptionId": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    },
                    "CertificateAssetName": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    }
                }
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/connectionTypes",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureServicePrincipal')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "isGlobal": true,
                "fieldDefinitions": {
                    "ApplicationId": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    },
                    "TenantId": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    },
                    "CertificateThumbprint": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    },
                    "SubscriptionId": {
                        "isEncrypted": false,
                        "isOptional": false,
                        "type": "System.String"
                    }
                }
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AuditPolicyDsc')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Azure')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Azure.Storage')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRM.Automation')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRM.Compute')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRM.Profile')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRM.Resources')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRM.Sql')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureRM.Storage')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/ComputerManagementDsc')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/GPRegistryPolicyParser')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Microsoft.PowerShell.Core')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Microsoft.PowerShell.Diagnostics')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Microsoft.PowerShell.Management')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Microsoft.PowerShell.Security')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Microsoft.PowerShell.Utility')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Microsoft.WSMan.Management')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/Orchestrator.AssetManagement.Cmdlets')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/PSDscResources')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/SecurityPolicyDsc')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/StateConfigCompositeResources')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/xDSCDomainjoin')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/xPowerShellExecutionPolicy')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/modules",
            "apiVersion": "2015-10-31",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/xRemoteDesktopAdmin')]",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "contentLink": {}
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/runbooks",
            "apiVersion": "2018-06-30",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureAutomationTutorial')]",
            "location": "westus",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "runbookType": "GraphPowerShell",
                "logVerbose": false,
                "logProgress": false,
                "logActivityTrace": 0
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/runbooks",
            "apiVersion": "2018-06-30",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureAutomationTutorialPython2')]",
            "location": "westus",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "runbookType": "Python2",
                "logVerbose": false,
                "logProgress": false,
                "logActivityTrace": 0
            }
        },
        {
            "type": "Microsoft.Automation/automationAccounts/runbooks",
            "apiVersion": "2018-06-30",
            "name": "[concat(parameters('automationAccounts_Surendhar_name'), '/AzureAutomationTutorialScript')]",
            "location": "westus",
            "dependsOn": [
                "[resourceId('Microsoft.Automation/automationAccounts', parameters('automationAccounts_Surendhar_name'))]"
            ],
            "properties": {
                "runbookType": "PowerShell",
                "logVerbose": false,
                "logProgress": false,
                "logActivityTrace": 0
            }
        }
    ]
}