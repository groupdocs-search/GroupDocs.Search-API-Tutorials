---
title: "Obtain Temporary License GroupDocs – Master Search Nodes (Java)"
description: "Learn how to obtain a temporary license for GroupDocs.Search, add directories to index, and add custom document attributes while managing Java search network nodes."
date: "2026-07-02"
weight: 1
url: "/java/search-network/master-groupdocs-search-java-network-nodes/"
keywords:
- obtain temporary license groupdocs
- add directories to index
- add custom document attributes
type: docs
schemas:
- type: TechArticle
  headline: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  dateModified: '2026-07-02'
  author: GroupDocs
- type: HowTo
  name: Obtain Temporary License GroupDocs – Master Search Nodes (Java)
  description: Learn how to obtain a temporary license for GroupDocs.Search, add directories
    to index, and add custom document attributes while managing Java search network
    nodes.
  steps:
  - name: Configure Search Network
    text: The `configureSearchNetwork` function prepares the configuration object
      necessary for deploying nodes. `Configuration` is a class that holds all settings
      such as index folder, network ports, and node roles. - **Parameters:** The base
      path and port are used to locate resources and establish communica
  - name: Deploy Nodes
    text: 'The `deploySearchNetwork` function initializes and returns an array of
      search network nodes. `SearchNetworkNodes` represents each node instance that
      participates in the distributed search cluster. - **Parameters:** Base path,
      port, and configuration are used to determine the deployment environment. '
  - name: Subscribe to Master Node Events
    text: '- **Purpose:** This step ensures that you are notified of significant events
      or changes within your search network.'
  - name: Get Indexed Documents
    text: '- **Purpose:** Verifies the successful indexing of all necessary documents
      within your search network.'
  - name: Close All Nodes
    text: '`closeNodes` shuts down all active search nodes and releases allocated
      resources. - **Purpose:** Releases resources occupied by each node, ensuring
      a clean shutdown process.'
- type: FAQPage
  questions:
  - question: How long does a temporary license remain valid?
    answer: Temporary licenses are typically valid for 30 days, giving you ample time
      to evaluate the product.
  - question: Can I switch from a temporary to a full license without reinstalling?
    answer: Yes—replace the temporary license file with the full license file and
      restart your application.
  - question: Do I need to re‑index documents after applying a new license?
    answer: No, the index remains intact; the license only governs usage rights.
  - question: What happens if I forget to close nodes?
    answer: Unreleased resources may lead to memory leaks; always invoke `closeNodes`
      during shutdown.
  - question: Is it possible to add more than one custom attribute per document?
    answer: Absolutely—call `addAttribute` multiple times with different attribute
      names.
---

# Obtain Temporary License GroupDocs – Master Search Nodes (Java)

In this comprehensive guide you’ll **obtain a temporary license for GroupDocs.Search**, configure a multi‑node search network, and learn how to **add directories to index** and **add custom document attributes** using Java. Whether you’re building an enterprise document‑management system or a searchable product catalog, mastering these steps lets you evaluate the platform without restrictions and scale your search capabilities quickly.

## Quick Answers
- **What is the first step to start using GroupDocs.Search?** Obtain a temporary license from the GroupDocs portal.  
- **Which Maven repository hosts the library?** `https://releases.groupdocs.com/search/java/`.  
- **How do I add directories to index?** Call the `addDirectoriesToIndex` helper on the master node.  
- **Can I add custom document attributes?** Yes—invoke `addAttribute` with the document key and attribute name.  
- **How do I shut down nodes cleanly?** Invoke `closeNodes` to release resources.

## What is a temporary license and why do I need it?
A temporary license lets you evaluate GroupDocs.Search without any evaluation limitations. It’s perfect for development, testing, or proof‑of‑concept projects before committing to a full purchase. The license grants full‑feature access for a limited period, allowing you to benchmark performance, test integration points, and ensure the solution meets your requirements without financial commitment.

## Prerequisites

Before we begin, ensure you have the following prerequisites in place:

### Required Libraries and Dependencies
To work with GroupDocs.Search for Java, include the necessary Maven dependencies:
```xml
<repositories>
   <repository>
      <id>repository.groupdocs.com</id>
      <name>GroupDocs Repository</name>
      <url>https://releases.groupdocs.com/search/java/</url>
   </repository>
</repositories>

<dependencies>
   <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-search</artifactId>
      <version>25.4</version>
   </dependency>
</dependencies>
```  
You can also download the latest version directly from [GroupDocs.Search for Java releases](https://releases.groupdocs.com/search/java/).

### Environment Setup
- Ensure you have a compatible JDK installed (Java 8 or later).  
- Set up your IDE to support Maven projects.

### Knowledge Prerequisites
A basic understanding of Java programming and familiarity with Maven project management will be beneficial. If you're new to these concepts, consider exploring introductory resources to get started.

## How to obtain a temporary license
A temporary license is obtained by visiting the GroupDocs portal, completing a short request form, and placing the received `.lic` file into your project’s `resources` folder. Then initialize the license with a few lines of code (see the snippet below). For the request form, use the official page: [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/).

## Setting Up GroupDocs.Search for Java

### Installation Information
To begin using GroupDocs.Search for Java in your project, follow the Maven steps above or download the latest version directly from the official releases page.

#### License Acquisition Steps
1. **Free Trial** – Explore the features without any commitment.  
2. **Temporary License** – Obtain a short‑term key for testing (see the section above).  
3. **Purchase** – For production use, buy a full license from the **[GroupDocs Purchase Page](https://purchase.groupdocs.com/)**.

### Basic Initialization and Setup
Initialize your project with GroupDocs.Search as follows:
```java
Configuration config = new Configuration();
// Set up basic configuration settings for your application.
```  
This initialization step is crucial to ensure that all components function seamlessly within your search network.

## Implementation Guide
Now, let's break down the process into manageable sections, each focusing on a specific feature of deploying and managing search network nodes.

### Feature 1: Configuration Setup
**Overview:** Setting up the configuration for your search network is the first step in deploying nodes. This setup involves specifying paths and ports critical for node deployment.

#### Implementation Steps:
##### Step 1: Define Base Path and Port
```java
String basePath = "/path/to/config";
int basePort = 8080;
```  

##### Step 2: Configure Search Network
The `configureSearchNetwork` function prepares the configuration object necessary for deploying nodes.  
`Configuration` is a class that holds all settings such as index folder, network ports, and node roles.  
```java
Configuration config = configureSearchNetwork(basePath, basePort);
```  
- **Parameters:** The base path and port are used to locate resources and establish communication channels.  
- **Return Value:** A configured `Configuration` object tailored to your deployment needs.

### Feature 2: Search Network Deployment
**Overview:** Deploying nodes is essential for scaling your search capabilities across different environments or segments of data.

#### Implementation Steps:
##### Step 1: Deploy Nodes
The `deploySearchNetwork` function initializes and returns an array of search network nodes.  
`SearchNetworkNodes` represents each node instance that participates in the distributed search cluster.  
```java
SearchNetworkNode[] nodes = deploySearchNetwork(basePath, basePort, config);
```  
- **Parameters:** Base path, port, and configuration are used to determine the deployment environment.  
- **Return Value:** An array containing initialized `SearchNetworkNodes`.

### Feature 3: Subscribing to Network Events
**Overview:** Monitoring your search network's activities is crucial for maintaining optimal performance and reliability.

#### Implementation Steps:
##### Step 1: Subscribe to Master Node Events
```java
subscribeToNodeEvents(nodes[0]); // Assuming the master node is at index 0.
```  
- **Purpose:** This step ensures that you are notified of significant events or changes within your search network.

### Feature 4: Indexing Documents
**Overview:** Adding directories containing documents to be indexed allows for efficient data retrieval across your network.

#### How to add directories to index
`addDirectoriesToIndex` is a helper method that registers folder paths for indexing on the master node.  
```java
addDirectoriesToIndex(nodes[0]); // Use the master node for indexing.
```  
- **Purpose:** Facilitates quick access and searchability of all documents within specified directories.

### Feature 5: Adding Attributes to Documents
**Overview:** Custom attributes enhance document metadata, making searches more flexible and informative.

#### How to add custom document attributes
`addAttribute` adds a custom metadata attribute to a specified document in the index.  
```java
addAttribute(nodes[0], "documentKey123", "customAttribute");
```  
- **Parameters:** Specify the node, document key, and attribute to be added.  
- **Purpose:** Extends the search functionality by enriching documents with additional metadata.

### Feature 6: Retrieving Indexed Documents
**Overview:** Efficiently retrieve and list indexed documents to ensure data accuracy and completeness.

#### Implementation Steps:
##### Step 1: Get Indexed Documents
```java
getIndexedDocuments(nodes[0]);
```  
- **Purpose:** Verifies the successful indexing of all necessary documents within your search network.

### Feature 7: Closing Network Nodes
**Overview:** Properly closing nodes is crucial for resource management and preventing memory leaks.

#### Implementation Steps:
##### Step 1: Close All Nodes
`closeNodes` shuts down all active search nodes and releases allocated resources.  
```java
closeNodes(nodes);
```  
- **Purpose:** Releases resources occupied by each node, ensuring a clean shutdown process.

## Why use a temporary license for GroupDocs.Search?
A temporary license provides **full‑feature access for 30 days** and supports up to **50,000 indexed documents** without performance throttling. This lets you benchmark indexing speed, query latency, and scalability on real‑world data before purchasing a production license. It also removes evaluation watermarks, giving you a true representation of the final product’s capabilities.

## Common Use Cases
1. **Enterprise Document Management** – Index millions of internal files across departments, enabling instant full‑text search.  
2. **E‑commerce Platforms** – Build a searchable product catalog that spans multiple warehouses and third‑party feeds.  
3. **Legal Firms** – Organize case files, contracts, and evidence with custom metadata for rapid retrieval.

Integration possibilities with other systems include CRM platforms, content management systems (CMS), and data analytics tools, leveraging the robust indexing and searching features provided by GroupDocs.Search for Java.

## Performance Considerations
To optimize performance when using GroupDocs.Search for Java:
- **Optimize Configuration** – Tailor your configuration settings to match your specific deployment environment.  
- **Monitor Resource Usage** – Regularly check CPU, memory, and I/O to prevent bottlenecks or memory leaks.  
- **Follow Best Practices** – Adhere to Java memory‑management guidelines, ensuring efficient utilization of system resources.

## Frequently Asked Questions

**Q: How long does a temporary license remain valid?**  
A: Temporary licenses are typically valid for 30 days, giving you ample time to evaluate the product.

**Q: Can I switch from a temporary to a full license without reinstalling?**  
A: Yes—replace the temporary license file with the full license file and restart your application.

**Q: Do I need to re‑index documents after applying a new license?**  
A: No, the index remains intact; the license only governs usage rights.

**Q: What happens if I forget to close nodes?**  
A: Unreleased resources may lead to memory leaks; always invoke `closeNodes` during shutdown.

**Q: Is it possible to add more than one custom attribute per document?**  
A: Absolutely—call `addAttribute` multiple times with different attribute names.

---

**Last Updated:** 2026-07-02  
**Tested With:** GroupDocs.Search for Java 25.4  
**Author:** GroupDocs

## Related Tutorials

- [Deploy a Search Network Node in .NET using GroupDocs for Efficient Document Indexing and Retrieval](/search/net/search-network/groupdocs-net-deploy-search-node-index-retrieve/)
- [How to Implement a Search Network with GroupDocs.Search in .NET for Document Management Systems](/search/net/search-network/implement-search-network-groupdocs-dotnet/)
- [Configuring Aspose.Search Network & Adding Document Attributes with GroupDocs.Redaction for .NET: A Comprehensive Guide](/search/net/search-network/aspose-search-network-groupdocs-redaction-net-guide/)
