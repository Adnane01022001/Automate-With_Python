<h1>Access Control IP Check Tool.</h1>

<h2>Description</h2>
As a security professional working at my company. As part of my job, I am required to regularly update a file that identifies the employees who can access restricted content. The contents of the file are based on who is working with personal patient records. Employees are restricted access based on their IP address. There is an allow list identified in the "allow_list.txt" file for IP addresses permitted to sign into the restricted subnetwork. There's also a remove list that identifies which employees you must remove from this allow list.


To automate this process, I created an algorithm using python to check whether the "allow_list.txt" contains any IP addresses identified on the remove list. If so, I should remove those IP addresses from the file containing the allow list.
<br />

<h2>Languages and Utilities Used</h2>

- <b>Python</b> 

<h2>Open the file that contains the allow list:</h2>
For the first part of the algorithm, I opened the "allow_list.txt" file. First, I assigned this
file name as a string to the import_file variable:

```python
# Assign 'import_file' to the name of the file
import_file = 'allow_list.txt' 
```
Then I used the With statement to open the file

```python
with open(import_file, "r") as file :
```

In my algorithm, the with statement is used with the .open() function in read mode to open the allow list file for the purpose of reading it. The purpose of opening the file is to allow me to access the IP addresses stored in the allow list file. The open function has two parameters, the first specifies the file to import, and the second indicates what we want to do with the file. In this case, "r" indicates I want to read it.

<h2>Read the file contents</h2>
In order to read the file contents , I used the .read() method to convert the file to a string.

```python
with open(import_file, "r") as file:
    ip_addresses = file.read()

```

When using an .open() function that includes the argument "r" for “read,” I can call the .read() function in the body of the with statement. The .read() method converts the file into a string and allows me to read it. I applied the .read() method to the file variable identified in the with statement. Then, I assigned the string output of this method to the variable ip_addresses. 

<h2>Convert the String into a list</h2>
In order to remove the malicious Ip addresses from the allow list, I needed it to be in list format. Therefore, I used the .split() method to convert the ip_addresses string into a list.

```python
ip_addresses = ip_addresses.split()
```

The .split() function is called by appending it to a string variable. It works by converting the contents of a string to a list. The purpose of splitting ip_addresses into a list is to make it easier to remove IP addresses from the allow list. By default, the .split() function splits the text by whitespace into list elements.

<h2>Iterate Through and Remove IPs from the Remove List</h2>
My algorithm requires removing any IP address from the allow list, ip_addresses, that is also contained in remove_list.  Because there were not any duplicates in ip_addresses, I was able to use the following code to do this:

```python
for element in remove_list:
    if element in ip_addresses:
        ip_addresses.remove(element)
```
First, within my for loop, I created a conditional that evaluated whether or not the loop variable element was found in the ip_addresses list. I did this because applying .remove() to elements that were not found in ip_addresses would result in an error. 

Then, within that conditional, I applied .remove() to ip_addresses. I passed in the loop variable element as the argument so that each IP address that was in the remove_list would be removed from ip_addresses.

<h2>Update the file with the revised list of IP addresses</h2>
As a final step in my algorithm, I needed to update the allow list file with the revised list of IP addresses. To do so, I first needed to convert the list back into a string. I used the .join() method for this:

```python
# Convert 'ip_addresses' back to a string
ip_addresses = "\n".join(ip_addresses)
```

The .join() method combines all items in an iterable into a string. The .join() method is applied to a string containing characters that will separate the elements in the iterable once joined into a string. In this algorithm, I used the .join() method to create a string from the list ip_addresses so that I could pass it in as an argument to the .write() method when writing to the file "allow_list.txt". I used the string ("\n") as the separator to instruct Python to place each element on a new line.

Then, I used the with statement with the .write() method to update the file:

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

This time, I used a second argument of "w" with the open() function in my with statement. This argument indicates that I want to open a file to write over its contents. When using this argument "w", I can call the .write() function in the body of the with statement. The .write() function writes string data to a specified file and replaces any existing file content.

<h2>Summary</h2>
</br>I created an algorithm that removes IP addresses identified in a remove_list variable from the "allow_list.txt" file of approved IP addresses. This algorithm involved opening the file, converting it to a string to be read, and then converting this string to a list stored in the variable ip_addresses. I then iterated through the IP addresses in remove_list. With each iteration, I evaluated if the element was part of the ip_addresses list. If it was, I applied the .remove() method to it to remove the element from ip_addresses. After this, I used the .join() method to convert the ip_addresses back into a string so that I could write over the contents of the "allow_list.txt" file with the revised list of IP addresses.
