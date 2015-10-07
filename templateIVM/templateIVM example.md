The page model returned by createPageModel() is the following:


	pm = {
		map_related : {
			x : 45,	    // this will be used for lat
			y : 73,     // this will be used for lng
			z : 5       // this will be used for the zoom property
		},
		earthquakes : [
			{
				location: {
					x : 10,
					y : 11,
				}
				magnitude : 9.2,
				scale : "Richter",
				date : "06/22/1989",
				time : "15:43",
				affected_cities: [
					"La Jolla", 
					"Del Mar",
					"Solana Beach",
					"Encinitas",
					"Carlsbad",
					"Vista",
					"San Marcos",
					"Escondido"
				]
			},
			{
				location: {
					x : 8,
					y : 16,
				}
				magnitude : 5.5,
				scale : "Richter",
				date : "01/13/1995",
				time : "19:48",
				affected_cities: [
					"Newark", 
					"Manhattan",
					"Brooklyn",
					"Elmont",
					"Queens",
					"Astoria",
					"Woodside",
					"University Heights"

			}
		
		]
	}
	
The template language is:

	<% refresh pm  = createPageModel() %>
	<% unit google.maps.Maps %> {
		options : {
			center : {
				direct : {
					latitude : <%= pm.map_related.x %>,
					longitude : <%= pm.map_related.y %>
				},
				zoom : <%= pm.map_related.z %>
			},
		},
		markers : [
			<% for earthquake in pm.earthquakes %>
				{
					position : {
						direct : {
							latitude : <%= earthquake.location.x %>,
							longitude : <%= earthquake.location.y %>
						}
					},
					infowindow: {
						content : 
							<% html %>
								<table> 
                					<tr>
                    					<th> Affected Areas </th>
                					</tr>
                					<% for city in earthquake.affected_cities %>
                    					<tr>
                        					<td> <%= city %></td>
                    					</tr>
                					<% end for %>

            					</table>   
							<% end html %>
					}
				}
		]
	
	}
	
	
