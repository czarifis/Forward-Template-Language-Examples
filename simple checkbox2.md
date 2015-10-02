## Some comments for this example:

Assume that students look like this:
students: [
	{ sid: 10, name: 'x' },
    { sid: 20, name: 'y' }
]
selected_values : {
	10: false,
	20: false
}
Therefore selected_values will look like this:
selected_values 

	<% template root() %>
		<% refresh students = getStudents() %>
		<% init selected_values = {} %>
		<% for student in students %>
			<% init selected_values[student.sid] = false %>
			<% unit html.Checkbox %>
        	{
            	checked : <% selected_values[student.sid] %>
        	}
			<% end unit %>
		<% end for %>
		<button onclick="postData(selected_values)">Click me</button>
	<% end template %>