({
    doInit : function(component) {
        var action = component.get("c.getAllFields");
        action.setParams({
            sObjectName: component.get("v.sObjectName"),
            selectedField: component.get("v.fieldName")
        });
        action.setCallback(this, function(response) {
            var responselist = response.getReturnValue();
            var fieldData =[];
            for(var i= 0;i<responselist.length;i++){
                
                for(var j =0 ;j<responselist[i].fieldAllInfo.length;j++){
                    if(responselist[i].isLookup == 'isNotLookup'){ 
                        component.set("v.showPickListFields",false);
                        component.set("v.showAllFields",true);
                        fieldData.push({
                            fieldtype:responselist[i].fieldAllInfo[j].split(',')[0],
                            fieldLabel:responselist[i].fieldAllInfo[j].split(',')[1],
                            fieldsName:responselist[i].fieldAllInfo[j].split(',')[2]
                        });
                    }
                    /*else if(responselist[i].fieldAllInfo[j].split(',')[0]  == 'multipiclist'){
                        
                        
                        }*/
                    else{
                        
                        component.set("v.showPickListFields",true);
                        component.set("v.showAllFields",false);
                        fieldData.push({
                            fieldtype:responselist[i].fieldAllInfo[j].split(',')[0],
                            fieldLabel:responselist[i].fieldAllInfo[j].split(',')[1],
                            fieldsName:responselist[i].fieldAllInfo[j].split(',')[2],
                            fieldValue:responselist[i].lookUpFieldValues
                        });
                    }
                    
                }
                for(var j =0 ;j<responselist[i].lookUpFieldValues.length;j++){
                    fieldData.push({
                        fieldValue:responselist[i].lookUpFieldValues[j]
                    })
                    console.log(responselist[i].lookUpFieldValues[j]);
                }
            }
            console.log(fieldData);
            component.set("v.fieldInformationList", fieldData);
        })
        $A.enqueueAction(action);
    }
})
