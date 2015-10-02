

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
		<% html %> <!-- This is not even necessary, right?-->
			<% for element in labels %>
				<% unit html.Checkbox %>{
                  	checked : <% bind element.checked %> <!-- I copied this example from the tutorial I'm not sure how the "checked :" is described by the BNF -->
            	}<% end unit %>
				<label><%=element.name %>  </label></br>
			<% end for %>
		<% end html %>
		
		<div> <!-- Other Static HTML content --> </div>
	<% end template %>