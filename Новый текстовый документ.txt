<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="1.0"
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  
  <xsl:output method="xml" encoding="UTF-8" indent="yes"/>
  
  <xsl:template match="/">
    <items>
      <xsl:call-template name="process-comments">
        <xsl:with-param name="node" select="ul"/>
        <xsl:with-param name="parentid" select="0"/>
      </xsl:call-template>
    </items>
  </xsl:template>
  
  <xsl:template name="process-comments">
    <xsl:param name="node"/>
    <xsl:param name="parentid"/>
    
    <xsl:for-each select="$node/li[@data-id]">
      <item id="{@data-id}" parentid="{$parentid}">
        <xsl:attribute name="author">
          <xsl:value-of select="normalize-space(b)"/>
        </xsl:attribute>
        <xsl:value-of select="normalize-space(span)"/>
      </item>
      
      <xsl:if test="ul">
        <xsl:call-template name="process-comments">
          <xsl:with-param name="node" select="ul"/>
          <xsl:with-param name="parentid" select="@data-id"/>
        </xsl:call-template>
      </xsl:if>
    </xsl:for-each>
  </xsl:template>
  
</xsl:stylesheet>