pipeline {
   agent any
		stages	{
			stage("Check commit")	{
				steps {
              			sh '''
                			# Get the list of all the files that are being committed
					difflist_for_one=$(git diff HEAD^ HEAD --name-only)
                			difflist_for_two=$(git diff HEAD~3..HEAD --name-only)										
                			difflist_for_three=$(git diff HEAD~3..HEAD --name-only)


					# Loop through each file in the difflist, including files in subdirectories
					for file in $difflist_for_one; do    			
						# Check if the file name starts with "tjx_"
    						if echo "$file" | grep -q "tjx_"; then
        						echo "$file follows the naming convention"
    						else
						    # Check if the file name is in the exception list
        						if grep -q $file exception_list.txt; then
            							echo "$file is in exception list";
							else
        							echo "ERROR: $file does not begin with tjx_";
							fi;
    						fi;
					done
                			'''       
                }
			}
    }
}
