({
    ({
                            fieldtype:responselist[i].fieldAllInfo[j].split(',')[0],
                            fieldLabel:responselist[i].fieldAllInfo[j].split(',')[1],
                            fieldsName:responselist[i].fieldAllInfo[j].split(',')[2]
                    
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
