---
page_css:
- "https://cdn.datatables.net/2.3.5/css/dataTables.dataTables.min.css"
---


<script src="https://code.jquery.com/jquery-3.7.1.js" crossorigin=""></script>
<script src="https://cdn.datatables.net/2.3.5/js/dataTables.min.js" crossorigin=""></script>

## SHAREing HPC Testbeds

UK researchers have access to a vast number of testbeds and machines
where they can quickly get access and trial new codes or ideas.
Some of these machines have been procured through governmental grants
such as the ExCALIBUR H&ES programme,
some universities open up their systems to UKRI-eligible colleagues,
and some commercial providers grant access to their systems in the Cloud,
too.
Unfortunately,
it is sometimes difficult to keep track of all the different opportunities.
This page collects systems as well as some meta information
such that it is easier for researchers to find the right system for the right purpose.

For each system,
click its name to find out more about that system.

{% assign columns = "System name,Status,Category,Focus,Focus area,Grouping,Funders,Nodes,Accelerators,Accelerator count per node,Manufacturer,Scheduler,Interconnects,Reference" | split: "," %}

<p style="margin-bottom: 0px; padding-bottom: 0px;">
  <a class="toggle-visibility-controls">
    Show/hide columns
    <span class="visibility-control-shown" style="display: none;">▴</span>
    <span class="visibility-control-hidden" style="display: inline;">▾</span>
  </a>
</p>

<div class="visibility-controls" style="display: none; padding-top: 0px;">
{% for column in columns %}
  <a class="toggle-visibility-column column-shown" data-column="{{ forloop.index0 }}">{{ column }}</a>
  {% unless forloop.last %}•{% endunless %}
{% endfor %}
</div>


<table id="systems" class="display">
  <thead>
    <tr>
{% for column in columns %}
      <th>{{ column }}</th>
{% endfor %}
    </tr>
  </thead>
  <tbody>
    {% for system in site.systems %}
      {% if system.url == "/systems/system-template/" %}
        {% continue %}
      {% endif %}
    <tr>
      <td><a href="{{ site.baseurl }}{{ system.url }}">{{ system.name }}</a></td>
      <td>{{ site.data.statuses[system.status]["shortdescription"] }}</td>
      <td>{{ site.data.categories[system.category]["shortdescription"] }}</td>
      <td>{{ site.data.focuses[system.focus]["shortdescription"] }}</td>
      <td>{{ system.focus-detail }}</td>
      <td>{{ system.grouping }}</td>
      <td>{{ system.funders | join: "<br>" }}</td>
      <td>{{ system.nodes }}</td>
      <td>{{ system.accelerators | join: "<br>" }}</td>
      <td>{{ system.accelerator-count }}</td>
      <td>{{ system.manufacturer }}</td>
      <td>{{ system.scheduler }}</td>
      <td>{{ system.interconnects | join: "<br>" }}</td>
      <td><a href="{{ system.reference }}">Link</a></td>
    </tr>
    {% endfor %}
  </tbody>
  <tfoot> <!-- add empty space to indicate we want to have a filter drop-down -->
    <th></th>
    <th>&nbsp;</th> <!-- Status -->
    <th>&nbsp;</th> <!-- Categories -->
    <th>&nbsp;</th> <!-- Focus -->
    <th>&nbsp;</th> <!-- Focus detail -->
    <th>&nbsp;</th> <!-- Grouping -->
    <th></th>
    <th></th>
    <th></th>
    <th></th>
    <th>&nbsp;</th> <!-- Manufacturer -->
    <th>&nbsp;</th> <!-- Scheduler -->
    <th></th>
    <th></th>
  </tfoot>
</table>

<script>
let table = new DataTable(
  '#systems',
  {
    initComplete: function () {
        this.api()
            .columns()
            .every(function () {
                let column = this;

                if (column.footer().innerHTML == '<div class="dt-column-footer"><span class="dt-column-title"></span></div>') {
                  return;
                }

                // Create select element
                let select = document.createElement('select');
                select.style.width = "100%";
                select.add(new Option(''));
                column.footer().replaceChildren(select);

                // Apply listener for user change in value
                select.addEventListener('change', function () {
                    column
                        .search(select.value, {exact: true})
                        .draw();
                });

                // Add list of options
                column
                    .data()
                    .unique()
                    .sort()
                    .each(function (d, j) {
                        select.add(new Option(d));
                    });
            });
    }
  }
);

document.querySelectorAll('a.toggle-visibility-column').forEach((eventList) => {
    eventList.addEventListener('click', function (event) {
        event.preventDefault();
        let element = event.target;

        let columnIdx = element.getAttribute('data-column');
        let column = table.column(columnIdx);

        // Toggle the column visibility and colour-code the control to indicate this
        if (column.visible()) {
          element.classList.add('column-hidden');
          element.classList.remove('column-shown');
          column.visible(false);
        } else {
          element.classList.remove('column-hidden');
          element.classList.add('column-shown');
          column.visible(true);
        }
    });
});

// Toggle the visibility of the visibility controls
document.querySelector('a.toggle-visibility-controls').addEventListener('click', function(e) {
    e.preventDefault();
    controls = document.querySelector('div.visibility-controls');
    if (controls.style.display == 'none') {
      controls.style.display = 'inline';
      document.querySelector('span.visibility-control-shown').style.display = 'inline';
      document.querySelector('span.visibility-control-hidden').style.display = 'none';
    } else {
      controls.style.display = 'none';
      document.querySelector('span.visibility-control-shown').style.display = 'none';
      document.querySelector('span.visibility-control-hidden').style.display = 'inline';
    }
});
</script>

## Disclaimer

This page is not yet complete,
and we plan to work towards precise guidelines
on what additional detail should be documented per cluster on such an overview page.

Is your system not included on this list?
Please [add it at the GitHub repository for this site][github]!

[github]: <https://github.com/SHAREing-dri/hpc-testbeds>
