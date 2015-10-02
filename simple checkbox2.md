## Some comments for this example:

Assume that students look like this:

	students: [
		{ sid: 10, name: 'x' },
	    { sid: 20, name: 'y' }
	]
	
Therefore selected_values will look like this:

	selected_values : {
		10: false,
		20: false
	}
	
1. We probably have to create some "magic" that converts numbers to strings (when used as attributes of an object)

 

		<% template root() %>
			<% refresh students = getStudents() %>
			<% init selected_values = {} %>
			<% for student in students %>
				<% init selected_values[student.sid] = false %>
				<% unit html.Checkbox %>
	        	{
		            	checked : <% selected_values[student.sid] %> <!-- There is some magic happening here check point # 1 -->
		        	}
				<% end unit %>
			<% end for %>
			<button onclick="postData(selected_values)">Click me</button>
		<% end template %>
