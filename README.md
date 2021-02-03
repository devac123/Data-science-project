devlop = true;
if(devlop){
    function clog(word){
        console.log(word);
    }
}


//clog("new crud");
// --------------------------------------------- first
function aj(){


$.ajax({
    type: "post",
    url: "/Controller/prodFieldsController.php",
    data: {fields : "fields"},   
    success: function (response) {
        RT = JSON.parse(response.trim());
        //clog(RT)
        
    },
    error : function(){
        //clog("ajax error in first ajex ")
    }

});

}

aj()
// -------------------------------------------------
 $(document).ready(function(){
        formField1  = {title : "name",   key : "name",     name : "name",     type:"text",  placeholder : "name", value :"",}
        formField2  = {title : "email",  key : "email",    name : "email",    type:"email",  placeholder : "email",  value :"",}
        formField31 = {title : "number",  key : "number",  name : "number",   type:"number",  placeholder : "number",  value :"",}
        formField32 = {title : "password",key : "password",name : "password", type:"password",  placeholder : "password",  value :"",}
        formField3  = {title : "phone",  key : "mobile",   name : "mobile",   type:"tel",  placeholder : "phone",  value :"",}
        formField4  = {title : "status", key : "status",   name : "status",   type:"status",  placeholder : "status",  value :"",}
        formField51 = {title : "select", key : "select",   name : "select",   type:"select",  placeholder : "gender",  value :"",}   
        formField5  = {title : "gender", key : "check",   name : "gender",   type:"checkbox",  placeholder : "gender",  value :"",}   
        formField6  = {title : "file",   key : "file",     name : "file",     type:"file", }

        formField7 = {title : "is_male", key : "gender",   name : "is_male",   type:"radio" },

        formField8 = {title : "Submit", key : "send_btn",   name : "send_btn",   type:"btn" },

        fieldArr = [formField1,formField2,formField32,formField31,formField3,formField6,formField7,formField5,formField51,formField8 ]
             datafields = {fields : fieldArr }

        var inputTemplate = `<div class="form-group"> <label for="exampleInputEmail1">$fieldName$</label> <input   aria-describedby="emailHelp" $inputAttr$ >
        </div>`;

        datafields['fields'].forEach(function(entry){
            tempfields = "";
            tempfields += ` data-key = "${entry['key']}"`;
            tempfields += ` placeholder = "${entry['placeholder']}"`;
            tempfields += ` name  = "${entry['name']}"`;
            tempfields += ` type  = ${inputTypeAttr(entry['type'])}`;
            // console.log(tempfields);  
            updated_inputTemplate = inputTemplate.replace("$fieldName$",entry['title'])
            updated_inputTemplate = updated_inputTemplate.replace("$inputAttr$ ",tempfields) 
            $('.form-div').append(updated_inputTemplate)

        })

        childClass = $('.form-group .form-check-input');
        if(childClass){
            parent =  childClass.parent();
            parent.removeClass('form-group');
            parent.addClass('form-check')
        }
        childClass = $('.form-group .form-check-input');
        if(childClass){
            parent =  childClass.parent();
            parent.removeClass('form-group');
            parent.addClass('form-check')
        }
        


        $('input').each(function(e){
             type = $(this).attr('type');
             //clog(type);
             if(type == "submit" || type == "file"  ){
                 $(this).parent().children('label').remove()
             }

             else if(type == "radio" || type == "checkbox"){
                inputLabel =  '<label>is_male</label>';
                $(this).parent().children('label').remove()
                $(this).parent().append(inputLabel);
             }
             else if(type == "select") {
                 selectInput = $(`input[type="${type}"]`);
                 selectInput = selectInput.parent();
                 selectInput.children('label').remove()
                clas = $(selectInput).attr('class');
                data_group = $(this).attr('data-group')
                $(selectInput).replaceWith(`<select class = '${clas} form-select-lg mb-3' data-key = "select" type = '${$(this).attr('type')}' data-group = "${data_group}" ><option selected>Open this select menu</option></select>`);
             }
                
        });
        
        function inputTypeAttr(inputType)
            {
                attrtype = "";
                if (inputType == "text")
                {
                    attrtype  += '"text"';
                    attrtype  += ' pattern="[a-zA-Z]+$" ';   
                    attrtype  += ' maxlength="50" ';
                    attrtype  += ' minlength="4" ';
                    attrtype  += ' class="form-control" ';
                    attrtype  += ' data-group = "form_data" ';
                }
                else if(inputType == "email")
                {
                    attrtype  += '"email"';
                    attrtype  += ' pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$" ';
                    attrtype  += ' class="form-control" ';
                    attrtype  += ' data-group = "form_data" ';
                       
                }
                else if(inputType == "number")
                {
                    attrtype  += '"number"';
                    attrtype  += ' pattern="[a-z0-9._%+-]+@[a-z0-9.-]+\.[a-z]{2,4}$" ';
                    attrtype  += ' class="form-control" ';
                    attrtype  += ' data-group = "form_data" ';
                       
                }
                else if(inputType == "select"){
                    attrtype += '"select"';
                    attrtype += 'class="form-select"';
                    attrtype  += ' data-group = "form_data" ';
                 
                }
                else if(inputType == "tel")
                {  
                    attrtype += ' "text" ';
                    attrtype += ' pattern="[0-9]{10}" ';
                    attrtype += ' class="form-control" ';
                    attrtype  += ' data-group = "form_data" ';
                }
                else if(inputType == "password"){
                    attrtype +=  ' "password" '
                    attrtype  += ' class = "form-control" ';
                    attrtype  += ' data-group = "form_data" ';
                }
                else if(inputType == "radio")
                {
                    attrtype += ' "radio" ';
                    attrtype += ' class="form-check-input" ';
                    attrtype  += ' data-group = "form_data" ';
                }

                else if(inputType == "checkbox")
                {
                    attrtype += ' "checkbox" ';
                    attrtype += ' class="form-check-input" ';
                    attrtype  += ' data-group = "form_data" ';
                }
                else if(inputType == "file")
                {
                    attrtype += ' "file" ';
                    attrtype  += ' id="chooseFile" ';
                    attrtype  += ' class = "form-control-file" ';
                    attrtype  += ' data-group = "form_data" ';
                }

                else if(inputType == "btn"){
                    attrtype +=  ' "submit" '
                    attrtype  += ' value="submit" ';
                    attrtype  += ' class = "btn btn-primary" ';
                    attrtype  += ' data-sel-group = "form_data" ';
                }
                
                else if(inputType == "radio")
                {
                    attrtype  += '"radio" ';
                    attrtype  += ' id="radioBtn" ';
                    attrtype  += ' class = "form-check-input" ';
                    attrtype  += ' data-group = "form_data" ';
                    

                }
                else{
                    attrtype  += '"number" ';
                    attrtype  += ' min="0" ';
                    attrtype += ' max="120" ';
                }
                return attrtype;   
            }
        })

        
        
$(document).on("click", "*[name = send_btn]",function(){
    group = $(this).attr('data-sel-group');
    dataObj = {};
    clog($(`input[data-group = "${group}"]`))  
    $(`input[data-group = "${group}"]`).each(function(){
        dataObj[$(this).attr('data-key')] = $(this).val();

    })
    clog(dataObj)


});





