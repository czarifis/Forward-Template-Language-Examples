## Some comments for this example:

Assume that students look like this:

	students: [
		{ sid: '10', name: 'x' },
	    { sid: '20', name: 'y' }
	]
	
Therefore selected_values will look like this:

	selected_values : {
		'10': false,
		'20': false
	}
	
1. Notice that the sid in this case is a string, that's why we can use it as a key/attribute within the selected_values object. It might make sense to create some sort of "magic" that converts numbers to strings (when used as attributes of an object), to support this even if the sid(s) are numbers.

 

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
			<% unit html.button %>
				<% event onClick postData(selected_values)%>
				value : 'Click me'
			<% end unit %>
		<% end template %>
