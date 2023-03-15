# Re<?php
if(isset($_POST['submit'])) { // check if the form has been submitted
    $url = $_POST['url']; // get the URL from the form field
    $filename = basename($url); // extract the filename from the URL
    $file = fopen($url, 'r'); // open the remote file for reading
    if($file) {
        $local_file = fopen($filename, 'w'); // open a local file for writing
        if($local_file) {
            while(!feof($file)) { // read the remote file and write to local file
                fwrite($local_file, fread($file, 1024 * 8), 1024 * 8);
            }
            fclose($local_file); // close the local file
            echo "File downloaded successfully.";
        } else {
            echo "Unable to open local file for writing.";
        }
        fclose($file); // close the remote file
    } else {
        echo "Unable to open remote file for reading.";
    }
}
?>

<!-- HTML form to get the URL input -->
<form method="post">
    <label for="url">Enter URL:</label>
    <input type="text" name="url" id="url">
    <input type="submit" name="submit" value="Download">
</form>
mote-file
