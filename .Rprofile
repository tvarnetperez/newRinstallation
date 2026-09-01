setHook(hookName = "rstudio.sessionInit", value = function(newSession) {
  if (newSession && !is.na(rstudioapi::getActiveProject())) {
    rprofile_used <- Sys.getenv("R_PROFILE_USER")
    message("Setting default folder structure from .Rprofile file from the following path: ", rprofile_used)
    # Define the folder structure
    folders <- c(
      "scripts/functions",
      "inputs/data",
      "inputs/objects",
      "outputs/plots",
      "outputs/tables",
      "outputs/objects"
    )
    
    # Create only folders that do not already exist
    for (folder in folders) {
      if (!dir.exists(folder)) {
        dir.create(folder, recursive = TRUE)
        message("Created: ", folder)
      } else {
        message("Already exists: ", folder)
      }
    }
    cat("Folder structure created successfully.\n")
    
  }
}, action = "append")


# Wrapper for multiple inspecting function calls
# To use only interactively/in console
whatis <- function(x, print_str = TRUE){
  # Numeric aspects of the object
  numeric_vector <- c(capture.output(dim(x)), as.character(length(x)), is.atomic(x))
  names(numeric_vector) <- c("Dimension", "Length", "Atomic?")
  # Type, class and mode 
  character_vector <- c(class(x), mode(x), typeof(x))
  names(character_vector) <- c("Class", "Mode", "Type of")
  # Structure, since it has multiple elements
  structure <- capture.output(str(x))
  names(structure) <- "Structure"
  # Print a list with both vectors
  print(list(numeric_vector, character_vector, if(print_str == TRUE) structure))
}
