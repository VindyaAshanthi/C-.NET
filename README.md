# C-.NET
Assignment Work
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="Dahl.aspx.cs" Inherits="Dahl.Dahl" %>
<%@ Import Namespace="System.IO" %>
<%@ Import Namespace="System.Net" %>

<!DOCTYPE html>
<html lang="en">
<head runat="server">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.css">
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    <title>Potential Customer Tracking System</title>
</head>
<body>
    <div class="container">
        <div class="header">
            <img src="logo.png" alt="DAHL Logo" class="logo">
            <h1>Potential Customer Tracking System</h1>
        </div>

        <form class="form" runat="server" method="post">
            <div class="form-row">
                <div class="form-group">
                    <label for="city">City</label>
                    <select id="city" name="city">
                        <option value="Lahti" <% if (Request.Form["city"] == "Lahti") { %>selected<% } %>>Lahti</option>
                        <option value="Helsinki" <% if (Request.Form["city"] == "Helsinki") { %>selected<% } %>>Helsinki</option>
                        <option value="Tampere" <% if (Request.Form["city"] == "Tampere") { %>selected<% } %>>Tampere</option>
                        <option value="Rovaniemi" <% if (Request.Form["city"] == "Rovaniemi") { %>selected<% } %>>Rovaniemi</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="business-line">Business Line</label>
                    <select id="business-line" name="business-line">
                        <option value="construction" <% if (Request.Form["business-line"] == "construction") { %>selected<% } %>>Construction</option>
                        <option value="banking" <% if (Request.Form["business-line"] == "banking") { %>selected<% } %>>Banking</option>
                        <option value="retail" <% if (Request.Form["business-line"] == "retail") { %>selected<% } %>>Retail</option>
                    </select>
                </div>
            </div>
            <div class="form-row">
                <div class="form-group">
                    <label for="time-start">Time Start</label>
                    <input type="date" id="time-start" name="time-start" value="<%= Request.Form["time-start"] ?? "2024-01-01" %>">
                </div>
                <div class="form-group">
                    <label for="time-end">Time End</label>
                    <input type="date" id="time-end" name="time-end" value="<%= Request.Form["time-end"] ?? "2024-11-01" %>">
                </div>
                <div class="form-group">
                    <label for="max-results">Max Results</label>
                    <input type="number" id="max-results" name="max-results" min="1" max="10" value="<%= Request.Form["max-results"] ?? "10" %>">
                </div>
                <div class="form-group button-group">
                    <button type="submit">Search</button>
                </div>
            </div>
        </form>

        <table class="result-table">
            <thead>
                <tr>
                    <th>Business ID</th>
                    <th>Company Name</th>
                    <th>Address</th>
                </tr>
            </thead>
            <tbody>
    <% if (ViewState["Companies"] != null)
       {
           string[][] companies = (string[][])ViewState["Companies"];
           foreach (var company in companies)
           {
               if (company != null)
               { %>
                   <tr>
                       <td><%= company[0] %></td>
                       <td><%= company[1] %></td>
                       <td><%= company[2] %></td>
                   </tr>
               <% }
           }
       }
       else
       { %>
           <tr>
               <td colspan="3">No results to display</td>
           </tr>
       <% } %>
</tbody>
        </table>

        
</body>
</html>
