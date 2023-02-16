pipeline {
   agent any
		stages	{
			stage("Check commit")	{
				steps {
              			sh '''
                			# Get the list of all the files that are being committed
                			difflist=$(git diff HEAD^ HEAD --name-only)

                			# Loop through each file in the difflist
                    	for file in $difflist; do
    							      # Check if the file name starts with "tjx_"
    							      if ! find . -name "$file" | grep -qv tjx_; then
									         continue
    							      else
        							      # Check if the file name is in the exception list
        							      if grep -q $file exception_list.txt; then
            							    continue
									          else
										        # Return error message if the file name does not follow the naming convention
        								      echo "ERROR: $file does not begin with tjx_"
        								      exit 1
        							      fi;
    						      	fi;
                			done
                			'''       
                }
			}
    }
}
