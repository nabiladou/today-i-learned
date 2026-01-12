# CAP Theorem

The **CAP theorem** describes the trade-offs in a distributed system. It states that when your system is spread across multiple servers, you can only guarantee **two out of three properties** at the same time:

- **Consistency (C):** Every user sees the same data at the same time.  
- **Availability (A):** Every request gets a response, even if some servers are down.  
- **Partition tolerance (P):** The system keeps working even if some servers in the network cannot talk to each other.  

Since network partitions are always possible, most systems must choose between **Consistency** and **Availability**.

## Examples

- **Banking app (CP):** Prioritizes Consistency and Partition Tolerance. It’s better to be temporarily unavailable than to show the wrong account balance.  
- **Social media platform (AP):** Platforms like Facebook often choose Availability and Partition Tolerance. If there’s a network issue, you might see an older feed rather than getting an error.  
- **E-commerce website (Partition Tolerance example):** Imagine an online store with servers in different regions. If the European servers lose connection to the U.S. servers:  
  - Users in the U.S. can continue browsing and buying products.  
  - Users in Europe might see slightly outdated stock information, but the site doesn’t crash.  
  - Once the network is restored, the servers sync and update the data.  

This shows how partition tolerance allows a system to **keep working even when parts of the network fail**.
