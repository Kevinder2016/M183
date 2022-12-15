# Lern-Bericht
von Kevin Frühwirth

## Einleitung

Das Modul 183 erklärt, wie Sie Ihre Website sichern können und Sicherheitslücken zu minimieren. Dieser Lernbericht erklärt, wie Sie Ihre Website vor SQL-Injection-Angriffen schützen.

## Was habe ich gelernt?

In diesem Projekt habe ich gelernt, wie man PreparedStatements verwendet, um SQL-Interpreter-Injektionen abzufangen und so Websites davor zu schützen.

## Beschreibung
Falscher Code der in der Insecure App war (nicht sicher)

```java
      public int insert(News news) {
        final String sql = "INSERT INTO news (posted, header, detail, author, is_admin_news) VALUES ('" + new java.sql.Timestamp(news.getPosted().getTime()) + "','" + news.getHeader() + "','" + news.getDetail() + "','" + news.getAuthor() + "'," + (news.getIsAdminNews() ? "1" : "0") + ")";
        int id = 0;

        try (Statement stmt = DbAccess.getConnection().createStatement()) {
            stmt.execute(sql);
            id = stmt.getGeneratedKeys().getInt(1);
        } catch (SQLException e) {
            Logger.getLogger(NewsDAO.class.getName()).log(Level.SEVERE, null, e);
        }

        return id;

    }
```

Sicherer Code mit preparedStatemens

```java
        public int insert(News news) {
        final String sql = "INSERT INTO news (posted, header, detail, author, is_admin_news) VALUES (?, ?, ?, ?, ?)";
        int id = 0;

        try (Connection conn = this.connect();
                PreparedStatement pstmt = conn.prepareStatement(sql)) {
            pstmt.setTimestamp(1, new java.sql.Timestamp(news.getPosted().getTime()));
            pstmt.setString(2, news.getHeader());
            pstmt.setString(3, news.getDetail());
            pstmt.setString(4, news.getAuthor());
            pstmt.setString(5, (news.getIsAdminNews() ? "1" : "0"));
            pstmt.executeUpdate();
        } catch (SQLException e) {
            Logger.getLogger(NewsDAO.class.getName()).log(Level.SEVERE, null, e);
        }

        return id;

    }
```

Die Sicherheitslücke im obigen Codeabschnitt besteht darin, dass Sie sich als Administrator anzeigen lassen können, indem Sie einfach den Eingabewert manipulieren. Das ist hier natürlich harmlos und ändert nur die Farbe der Nachrichtenanzeige, aber wenn das auf einer echten Seite der Fall wäre, könnten dies grosse Folgen haben. Um den Benutzer in diesem Fall als Administrator anzuzeigen, müssen Sie das Eingabefeld auf der News-Page anpassen und folgendes hineinschreiben:

## Verifikation

Ich habe mithilfe der Informationen aus dem Auftrag und den zur Verfügung gestellten Powerpoints, verstanden, wie man eine SQL-Interpreter Injection auf einer Webseite abfangen kann anhand von preparedStatements und somit seine Website sicherer gestalten kann.

# Reflektion zum Arbeitsprozess

👍Ich habe den Auftrag besser verstanden als einige andere Aufträge in diesem Modul und die Anleitung/Aufgaben im Auftrag und der Powerpoint Präsentation waren Sehr verständlich.

👎Ich hatte sehr starke Konzentrationsprobleme da ich diese Aufträge wie auch viele andere Aufträge von Zuhause aus gelöst habe. Ich habe normalerweise schon Probleme mich zu konzentrieren Zuhause, aber durch die Baustelle, die zurzeit neben meinem Haus war, war es noch schwieriger.

**VBV**: ✍️ Ich möchte meine Konzentration im Fernunterricht möglichst steigern und ich nehme mir vor im Präsenzunterricht alles zu geben, da es mir dort deutlich leichter fällt mich zu konzentrieren.
