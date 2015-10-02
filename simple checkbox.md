## Some comments for this example:
* I'm assuming that we only have collecting data that we use for reporting as well. At this point it's not clear to me if IVM optimizations are supported to collecting variables.
* There is a slight issue with the BNF when we have: 
checked: <% bind element.checked %>
We only support:
'checked': <% bind element.checked %> 

		<% template index() %>
			<% init labels = [
				{
         	 		"name": "Car",
         	 		"checked": false
    			}, 
    			{
    		 		"name":"Motorcycle", 
    		 		"checked": false
    			},
    			{
    		 		"name":"Moped", 
    		 		"checked": false
    			},
    			{
    		 		"name":"Tractor", 
    		 		"checked": false
    			},
    			{
    		 		"name":"Motorcycle", 
    		 		"checked": false
    			},
    			{
    		 		"name":"Skateboard", 
    		 		"checked": false
    			},
    			{
    		 		"name":"Long board", 
    	 			"checked": false
    			},
    			{
    					"name":"Bicycle", 
    	 		"checked": false
    			}
    		]    		

    		%>
			<% html %> 
				<% for element in labels %>
					<% unit html.Checkbox %>{
                  		checked : <% bind element.checked %> <!-- I copied this example from the tutorial we have to make some arrangements to the BNF because it's not currently supported -->
            		}<% end unit %>
					<label><%=element.name %>  </label></br>
				<% end for %>
			<% end html %>
		
			<div> <!-- Other Static HTML content --> </div>
		<% end template %>