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
                            while read -r filename; do
                            # Check if the filename starts with the naming standard
                               # if [[ "$filename" == "${naming_standard}"* ]]; then
			        if echo "$filename" | grep -q "$naming_standard"; then
                                    echo "Filename $filename meets the naming standard."
                                else
                                    # Check if the filename is in the exception list
                                    if grep -q "$filename" CI/exception_list.txt; then
                                        echo "Filename $filename is in the exception list."
                                    else
                                        # Print an error message if the filename does not follow the naming convention
                                        echo "ERROR: $filename does not begin with $naming_standard"
                                        exit 1
                                    fi
                                fi
                            done < $filename_list
                			'''       
                }
			}
    }
}
