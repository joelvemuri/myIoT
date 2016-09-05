<% if (!App.configuration.get("isTBA")) { %>
<div class="list-group-item">
    <%
    var topContent = getTopContent();
    if (topContent != null && topContent.length > 0) {
    for (var i=0; i < topContent.length; i++) {
    var contentItem = topContent[i];
    if (contentItem.contentType == "textSection") {
    %>

    <div class="heading-20 padding-bottom-20"><%= contentItem.title %></div>
    <% for (var j=0; j < contentItem.paragraphs.length; j++) { %>

    <p><%= contentItem.paragraphs[j].text %>
        <%
        if (contentItem.paragraphs[j].desktopImageSrc != null && contentItem.paragraphs[j].desktopImageSrc != "") { %>
        <img src="<%= contentItem.paragraphs[j].desktopImageSrc %>" style="max-width:100%;margin: 10px 0 10px 0;"/>
        <%
        }
        if (contentItem.paragraphs[j].desktopIframeSrc != null && contentItem.paragraphs[j].desktopIframeSrc != "") { %>
        <div class="wrapper">
        <iframe class="framestyle<%=i%>" frameBorder="0" width="100%" scrolling="no" marginwidth="0" marginheight="0" vspace="0" hspace="0"
                src="<%= contentItem.paragraphs[j].desktopIframeSrc %>"/></div>
        <%
        }
        if (contentItem.paragraphs[j].videoIframeSrc != null && contentItem.paragraphs[j].videoIframeSrc != "") { %>
        <div class="">
        <iframe class="videoIframe" frameBorder="0" width="100%" scrolling="no" marginwidth="0" marginheight="0" vspace="0" hspace="0"
                src="<%= contentItem.paragraphs[j].videoIframeSrc %>"/></div>
        <%
        }
        %>
    </p>
    <%
    }
    %>

    <% } else if (contentItem.contentType == "showMore") { %>

    <div class="moreinfocontainer">
        <a class="showme" style="display: inline-block;" href="javascript:void(0)">Show me how</a>

        <div class="moreinfo">
            <% for (var j=0; j < contentItem.paragraphs.length; j++) { %>

            <%= contentItem.paragraphs[j].text %>
                <%
                if (contentItem.paragraphs[j].desktopImageSrc != null && contentItem.paragraphs[j].desktopImageSrc != "") { %>
                <div class="wrapper">
                    <img src="<%= contentItem.paragraphs[j].desktopImageSrc %>"
                     style="max-width:100%;margin: 10px 0 10px 0;"/>
                </div>
                <%
                }
                if (contentItem.paragraphs[j].desktopIframeSrc != null && contentItem.paragraphs[j].desktopIframeSrc != "") { %>
                <div class="wrapper">
                	<iframe class="framestyle<%=i%>" width="870" scrolling="<% getScrollingVal() %>" marginwidth="0" marginheight="0" vspace="0" frameborder="0" hspace="0" src="<%= contentItem.paragraphs[j].desktopIframeSrc %>"/>
                </div>
                <%
                }
                %>
            <%
            }

            %>
        </div>
    </div>
    <% }
    }
    }
    %>

    <% if (getBody() && getBody().trim() != "") { %>
    <div class="heading-10 padding-top-10 boldstyle padding-bottom-20">
        <%= getBody() %>
    </div>
    <% } %>

    <%
    if (getSelectionType() == "hyperlink") { %>
    <div id="options" style="font-weight:bold; margin-bottom: 10px">
        <%
        var signals = validSignals;
        for (i = 0; i < signals.length; i++) {
        %>
        <p>
            <a class="testClick" id="<%= signals[i].name  %>" href="javascript:void(0)">
                <%= signals[i].displayName %>
            </a>
        </p>
        <% } %>
    </div>
    <%
    }

    if (getSelectionType() === "radio") { %>

    <%
    var signals = validSignals, checked = "";
    for (i = 0; i < signals.length; i++ ) {
    checked = getCheckState(i);
    %>
    <div>
        <dl>
            <dt>
                <input class="radiobutton" type="radio" name="answer" id="radio-<%= signals[i].name  %>"
                       value="<%= signals[i].name  %>" <%= checked %>/>
            </dt>
            <dd>
                <h4><%= signals[i].displayName %></h4>
            </dd>

        </dl>
    </div>
    <% } %>


    <div class="btns">
        <a id="continueBtn" class="button base-blue tracklink next" href="javascript:void(0)"><%= getButton() %></a>
    </div>
    <% } %>

    <% if (getSelectionType() === "button") { %>
        <%
        var signals = validSignals;
        for (i = 0; i < signals.length; i++ ) {
        %>
        <div class="btns">
            <a id="<%= signals[i].name %>" href="<%= signals[i].name %>" class="button fixed-width"><%=
                signals[i].displayName %></a>
        </div>
        <% }
    } %>
</div>

<% } else { %>
<div id="workflow-question" class="workflow-question">
    <div class="colored-container">
        <span class="message"><%= getBody() %></span>
    </div>

    <%
    var steps = getSteps();
    for( i=0; i < steps.length; i++ ) {
    %>
    <div class="description">
        <div class="step_name"> <%= steps[i].name %></div>
        <div class="step_message"><p><i> <%= steps[i].message %> </i></p></div>
    </div>
    <%
    }
    %>

    <% if (getSelectionType() == "hyperlink") { %>
    <div id="options" style="font-weight:bold; margin-bottom: 10px">
        <%
        var signals = validSignals;
        for (i = 0; i < signals.length; i++) {
        %>
        <p>
            <a class="testClick" id="<%= signals[i].name  %>" href="javascript:void(0)">
                <%= signals[i].displayName %>
            </a>
        </p>
        <% } %>
    </div>
    <%
    } else if (getSelectionType() === "radio") { %>
    <div id="options" style="font-weight:bold; margin-bottom: 10px">
        <%
        var signals = validSignals, checked = "";
        for (i = 0; i < signals.length; i++ ) {
        checked = getCheckState(i);
        %>
        <input type="radio" name="answer" id="<%= signals[i].name  %>" value="<%= signals[i].name  %>" <%= checked %> />
        <label for="<%= signals[i].name  %>" style="float: none;"><%= signals[i].displayName %></label>
        <% } %>
    </div>
    <div id="buttons">
        <button class="button" id="continueBtn"><%= getButton() %></button>
    </div>
    <%
    } else if (getSelectionType() === "button") { %>
    <div id="buttons">
        <%
        var signals = validSignals;
        for (i = 0; i < signals.length; i++ ) {
        %>
        <button class="button" id="<%= signals[i].name  %>"><%= signals[i].displayName %></button>
        <% } %>
    </div>
    <% } %>
</div>
<% } %>
