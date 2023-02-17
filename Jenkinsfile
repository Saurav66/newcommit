pipeline {
   agent any
		stages	{
			stage("Check commit")	{
				steps {
              			sh '''
                             		# Set difflist based on the number of latest commits
                            		if [ $(git log --pretty=oneline | wc -l) -eq 1 ]; then
                                		difflist=$(git diff HEAD^ HEAD --name-only)
                            		elif [ $(git log --pretty=oneline | wc -l) -eq 2 ]; then
                                		difflist=$(git diff HEAD~2..HEAD --name-only)
                            		else
                                		difflist=$(git diff HEAD~3..HEAD --name-only)
                            		fi
				
					# Loop through each file in the difflist, including files in subdirectories
					for file in $difflist; do    			
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
