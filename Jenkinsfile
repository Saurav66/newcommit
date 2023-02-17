pipeline {
   agent any
		stages	{
			stage("Check commit")	{
				steps {
              			sh '''
                			# Get the list of all the files that are being committed
                			difflist=$(git diff HEAD^ HEAD --name-only)


					# Loop through each file in the difflist, including files in subdirectories
					for file in $difflist; do    			
						# Check if the file name starts with "tjx_"
    						if [ "$file" == "*tjx_" ]; then
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
