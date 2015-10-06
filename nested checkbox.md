

	<% template index %>
		<% init categories = [
    	{
    		"category_id" : "10",
    		"category_name" : "Gas powered",
    		"sub_elements" : [
            	{
            		"category_id" : "11",
                	"name": "Car"
            	},
            	{
            		"category_id" : "12",
            	    "name": "Motorcycle"
            	},
            	{
            		"category_id" : "13",
            	    "name": "Moped"
            	},
            	{
            		"category_id" : "14",
                	"name": "Tractor"
            	},
            	{
            		"category_id" : "15",
                	"name": "Motorcycle"
            	}
        	]
    	},
    	{	
    		"category_id" : "20",
    		"category_name" : "Human powered",
    		"sub_elements" : [
            	{
            		"category_id" : "21",
            	    "name": "Skateboard"
            	},
            	{
            		"category_id" : "22",
            	    "name": "Long board"
            	},
            	{
            		"category_id" : "23",
                	"name": "Bicycle"
            	}
        	]
    	}
		]	
    	%>
    	<% init categories_with_checked_vals = addBooleanVariable2Category(categories)
		<% html %>
			<% for category in categories_with_checked_vals%>
				% unit html.Checkbox %>{
                  	checked : <% bind category.checked %>
            	}<% end unit %>
				<label><%=element.name %>  </label></br>
				<% for subCategory in category.sub_elements%>
					% unit html.Checkbox %>{
                  		checked : <% bind category.checked %>
            		}<% end unit %>
				<label><%=element.name %>  </label></br>
			<% end for %>
		<% end html %>
		
		<div> <!-- Other Static HTML content --> </div>
	<% end template %>