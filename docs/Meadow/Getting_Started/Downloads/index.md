---
layout: Meadow
title: Downloads
subtitle: Guides and documentation for Meadow
---

<table>
  <tbody id="releases">
    <tr>
      <td>Date</td>
      <td>Release</td>
      <td>Meadow.OS</td>
      <td>Meadow.CLI</td>
    </tr>
  </tbody>
</table>



<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/
Meadow.Network_0.4.6.zip">Meadow.Network_0.4.6.zip</a></p>

<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/
Meadow.Network_0.4.5.zip">Meadow.Network_0.4.5.zip</a></p>

<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/
Meadow.Network_0.4.4.zip">Meadow.Network_0.4.4.zip</a></p>

<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/
Meadow.Network_0.4.3.zip">Meadow.Network_0.4.3.zip</a></p>

<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/
Meadow.Network_0.4.2.zip">Meadow.Network_0.4.2.zip</a></p>

<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/
Meadow.Network_0.4.1.zip">Meadow.Network_0.4.1.zip</a></p>

<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/Meadow.Network_0.4.0.zip">Meadow.Network_0.4.0.zip</a></p>


<p><a href="https://www.wildernesslabs.co/downloads?f=/Meadow_Beta/Meadow.Bcl_0.4.0.zip">Meadow.Bcl_0.4.0.zip</a></p>

<script language="javascript">
    fetch('https://www.wildernesslabs.co/api/releases')
    .then(response => response.json())
    .then(json => {
        var releases = document.getElementById('releases');
        json.forEach(function(item, index, array){
            var createdAt = moment(item.createdAt + 'Z'); // parse UTC
            var row = releases.insertRow();
            addCell(row, createdAt.format("MMM Do YYYY"));
            addCell(row, item.title);
            addCell(row, `<a href="${item.osUrl}">${item.osUrl ? item.osUrl.substring(item.osUrl.lastIndexOf('/')+1) : ''}</a>`);
            addCell(row, `<a href="${item.cliUrl}">${item.cliUrl ? item.cliUrl.substring(item.cliUrl.lastIndexOf('/')+1) : ''}</a>`);
        });
    });

    function addCell(row, inner){
        var cell = row.insertCell();
        cell.innerHTML = inner;
    }

</script>
