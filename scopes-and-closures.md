## Scopes
Things about scope normally people dont know: 
1. JS **compiles** you program first
2. Imagine like a 2 pass(is this the right term?) compiler thing.
3. First the compiler declares all the variable by making(compiler makes the scope manager?) various scope managers.
4. While declaring, all the variables are initialized with the value `undefined`.
5. Then in the second pass the engine ignores all the declarations part and for every identifier in the LHS of the code confirms from the scope manager for its existence. Here the scope manager behaves super weirdly 

#### The algorithm goes like that (assuming synatx is all correct):
1. For every line having `var`.
2. Check for its existence in the current scope.  
`Yes ==> END`  
`No ==> Go to step 2`
3. Check for its existence in the scope just nextly outer to the current scope, if its is not global scope.  
`Yes ==> END`  
`No ==> Go to step 2`
4. If it is the global scope and the variable is not found here also, declare the variable in the current scope.

##### NOTE: 
The second pass has the two parts, depending on the variable appearing on the LHS or the RHS of the statement.
LHS => Some value is being assigned to it
RHS => Its value is being refrenced

#### Second pass, LHS part
1. Checks for the identifier existence in the current scope.  
`Yes => Assigns the value`  
`No => Go to step 2`
2. Checks for the existence in the scope just outer to the current scope, if its not the global scope.  
`Yes => Assigns the value`  
`No => Go to step 2`
3. If it is the global scope and the identifier is still no found, **it just goes ahead and creates one in the global scope and assigns the value to it.**

#### Second pass, RHS part
1. Checks for the identifier existence in the current scope.  
`Yes => Assigns the value`  
`No => Go to step 2`
2. Checks for the existence in the scope just outer to the current scope, if its not the global scope.  
`Yes => Assigns the value`  
`No => Go to step 2`
3. If it is the global scope and the identifier is still no found, **it throws error**

##### NOTE:
The error maybe of two types: 
1. `TypeError`: When we try to access some property from it or we try to call it like a function. Error message may vary depending on the above mentioned two cases.
2. `ReferenceError`: In all other cases
