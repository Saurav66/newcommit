pipeline {
   agent any
		stages	{
			stage("Check commit")	{
				steps {
              			sh '''
                            # Get the list of all the files that are being committed
                		filename_list=$(git diff HEAD^ HEAD --name-only)

                            # Set the file naming standard
                            naming_standard="tjx_"

                            # Loop through each filename in filename_list
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
