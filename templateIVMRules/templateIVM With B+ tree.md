* The template is going to be the B++ tree that we will have to define (look at slides to see how it's being generated)
* constructPath(binding, path) is a function that takes a binding (source signature, target signature) and a source path and generates the target path 
* a path signature p* fully matches a path p if p*s' === ps and both s and s' are empty
* InstantiatePayload(template T, environment E, target diff t) is a function that takes the template, the environment and a target path and generates a payload:
		
		function InstantiatePayload(T,E,t)
			Create object O
			find node n in T with path signature that matches t
			Starting from n perform a breadth first traversal
				if a static path p is found that leads to a leaf l with static content then
					O.p = l
				if a static path p is found that leads to a leaf l with dynamic content (binding) then
					O.p = l.s/E
				if a static path p is found that leads to an internal node do:
					 O.p = InstantiatePayload(T, E, t.p)
				if a dynamic path p_i=[*_i] is found that leads to a super node l then
					for p in l.s/E
						if p leads to a leaf l with static content then
							O[p] = l
						if p leads to a super node, internal node or leaf with dynamic content l then
							O[p] = InstantiatePayload(T,E,t[p]))



		function IVM (Template T, Environment E, diff d)
			S <- empty bag
			for binding b(s, t) in T.binding_list 
				if d is an Update(e, u') and type of b is super node
					if s fully matches e then
						e' <- constructPath(b, e)
						u'' <- InstantiatePayload(T, E, e')
						S <- S \cup Update(e';u'')
				if d is an Update(el, u') and type of b is leaf node
					if s fully matches e (with l being a path/static path signature) and there is a 1-to-1 correspondence between *'s in s and t then 
							e' <- constructPath(b, e)
							S <- S \cup Update(e'l;u')
				if d is an Update(e, u') and type of b is leaf node
					if s fully matches el and there is a 1-to-1 correspondence between *'s in s and t (with l being a path/static path signature) then 
						e' <- constructPath(b, el)
						S <- S \cup Update(e';navigate(u', l))
				if d is an Update(e, u') 
					if s matches e and there is no 1-to-1 correspondence between all *'s in s and t then 
                    	t' = {}
                    	iterate over each step c of t
                        	if path step signature c is (a static path signature) or (an [*_i] that is also found in s)
                            	t' = t'c
                            else break
                        find node b' in T with path signature that matches t'
                        s' <- get source path signature of b'
						e'' = part of path e that is fully matched by s'
						e' <- constructPath(b', e'')
						u'' <- InstantiatePayload(T, E, e')
						S <- S \cup Update(e';u'')
				if d is an insert-array(e, u') and type of b is super node
					if s fully matches e then
						e' <- constructPath(b, e)
						u'' <- InstantiatePayload(T, E, e')
						S <- S \cup insert-array(e';u'')
				if d is an delete(e) and type of b is super node
					if s fully matches e then
						e' <- constructPath(b, e)
						S <- S \cup delete(e')
				if d is an append(e, u') and type of b is super node
					if s fully matches e[*_i] then
						e' <- constructPath(b, e)
						u'' <- InstantiatePayload(T, E, e')
						S <- S \cup insert-array(e';u'')
			return all diffs in S